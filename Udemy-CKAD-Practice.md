# Udemy CKAD Practice

*Notes from the [Udemy CKAD course](https://www.udemy.com/certified-kubernetes-application-developer)*

## YAML Manifests

All k8s definition files have four required sections:
* apiVersion
* kind
* metadata
* spec

## Environment Setup

Setup kubectl alias:
```sh
$ alias kc=kubectl
```

## 10. Pod

Create just a pod via imperative command with label:
```sh
$ kc run --generator=run-pod/v1 nginx --image=nginx -l tier=frontend
```

Create pod manifest for nginx:
```sh
$ kc run nginx --image=nginx --dry-run -o yaml
```

Get pod info:
```sh
$ kc describe po nginx-pod:
```

Get more details of pods:
```sh
$ kc get po -o wide
```

Update an existing pod from changed source yaml:
```sh
$ kc apply -f redis-pod.yaml
```

Get running pod defintion from k8s and edit/update:
```sh
$ kc get po <pod-name> -o yaml > pod-definition.yaml
$ vim pod-definition.yaml
$ kc apply -f pod-definition.yaml
```

Edit running pod definition directly:
```sh
$ kc edit po <pod-name>
```

Delete all pods in default namespace:
```sh
$ kc delete po --all
```

Shell into (if possible) a running pod:
```sh
$ kc exec -it pod-name /bin/sh (or /bin/bash, if available)
```

## 18. ReplicaSet

A template section under spec can define a child resource,
e.g., a pod resource under replicaSet's spec.template section.
Do not include apiVersion or kind in the template.

A replicaset requires the selector section with matchLabels defining
the pod label to replicate on. It is still required to include the
pod template even if the pods already exist before creating the
replicaset, as any scale-up of more or failed pods will be done
from this template.

Scale a replicaset to a different number of pods:
```sh
$ kc scale --replicas=X rs nginx-replicaset
```

Update a replicaset with the replace command via definition file:
```sh
$ kc replace -f replicaset-definition.yaml
```

Get definition file from kubectl:
```sh
$ kc get rs ngnix-replicaset -o yaml > nginx-replicaset.yaml
```

## 21. Deployment

Create deployment direct from kubectl:
```sh
$ kc run nginx --image=nginx
```

Create a deployment manifest with 4 replicas of nginx and save to a file:
```sh
$ kc run --generator=deployment/v1beta1 nginx --image=nginx --dry-run --replicas=4 -o yaml > nginx-deployment.yaml
```

Create a service with nodeport 30080 exposed for access:
```sh
$ kc create svc nodeport nginx --tcp=80:80 --node-port=30080 --dry-run -o yaml
```

Create a service onto a deployment:
```sh
$ kc expose deployment webapp --type=NodePort --port=8080 --name=webapp-service --dry-run -o yaml > webapp-service.yaml
$ vim webapp-service.yaml
  ports:
    nodePort: 30082
$ kc create -f webapp-service.yaml
```

## 25. Namespace 

View all resources that exist in namespace of current context:
```sh
$ kc get all
```

Switch context to a different namespace, and verify
```sh
$ kc config set-context $(kubectl config current-context) --namespace=elastic-stack
$ kc config view | grep namespace
```

## 33. ConfigMap

Create a configmap imperatively with literal values:
```sh
$ kc create cm cmname --from-literal=KEY=VALUE
```

Create a configmap imperatively with a key-value file:
```sh
$ kc create cm configmap-name --from-file=keyvalue.properties
```

Create a configmap declaratively from manifest file (uses a "data"
header instead of "spec" in the file):
```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: configmap-name
data:
  KEY1: value1
  KEY2: value2
```

Inject a configmap into a pod defintion:
```yaml
spec:
  envFrom:
    - configMapRef:
        name: configmap-name
```

## 35. Secret

To create a secret file, encode values in base64:
```sh
$ echo -n 'password' | base64
```

To decode hashed values:
```sh
$ echo -n 'hAsH3dPAssW0rD' | base64 --decode
```

To attach a secret to a pod:
```yaml
spec:
  envFrom:
    - secretRef:
        name: secret-name
```

## 39. securityContext

Set user at pod-level (if not set in container-level):
```yaml
spec:
  securityContext:
    runAsUser: 1001
```

Set user and capabilities at container level:
```yaml
spec:
  containers:
    - name: app-container
      securityContext:
        runAsUser: 1001
        capabilities:
          add:
            - "MAC_ADMIN"
```

## 41. ServiceAccount

Get list of service accounts:
```sh
$ kc get sa
```

Create a service account:
```sh
$ kc create sa sa-name
```
*(Note: RBAC is also needed to apply appropriate permissions to account, but that will be covered later.)*

Add a service account to a pod or deployment:
```yaml
spec:
  serviceAccount: sa-name
```

## 44. Resource Requirements

### resources.requests

Setting resource minimum requirements:
* `cpu` in number of cores (default: 0.5, for half-core or half-hyperthread)
* `memory` in bytes (default: 256Mi, for 256 megabytes)

```yaml
spec:
  containers:
  - name: app-container
    resources:
      requests:
        memory: "1Gi"
        cpu: 1
```

### resources.limits

Setting resource limits:
* `cpu` defaults to 1 core, throttled when trying to exceed
* `memory` defaults to 512Mi, terminated when exceeding

```yaml
spec:
  containers:
  - name: app-container
    resources:
      limits:
        memory: "2Gi"
        cpu: 2
```

## 46. Taints and Tolerations

Taint nodes to prevent intolerant pods from being scheduled on those nodes.
* `taint-effect` can be one of:
  * NoSchedule - applies to new pods being scheduled
  * PreferNoSchedule
  * NoExecute - will terminate and reschedule any pods on a newly tainted node that don't have the toleration
* Tolerations on pods do not guarantee that they are scheduled only on tainted nodes (NodeAffinity does this)

```sh
$ kc taint no node-name instanceType=Compute:PreferNoSchedule
```

Add tolerations to pods for being acceptable to schedule on tainted nodes:
```yaml
spec:
  tolerations:
  - key: "instanceType"
    operator: "Equal"
    value: "Compute"
    effect: "PreferNoSchedule"
```

Remove a taint from a node by key (and effect):
```sh
$ kc taint no node-name instanceType:PreferNoSchedule-
```

## 48. nodeSelector 

Label nodes for node selectors:
```sh
$ kc label no node-name memSize=Large
```

Set which nodes a pod would be nice to be scheduled on with `nodeSelector`:
```yaml
spec:
  nodeSelector:
    memSize: Large
```

## 49. nodeAffinity

Use `nodeAffinity` to get specific on pod-to-node scheduling preferences:
* `nodeAffinity` types available/planned:
  * `requiredDuringSchedulingIgnoredDuringExecution`
  * `preferredDuringSchedulingIgnoredDuringExecution`
  * `requiredDuringSchedulingRequiredDuringExecution`
* `operator`s available:
  * `In`
  * `NotIn`
  * `Exists`
  * (others in documentation)

```yaml
spec:
  affinity:
    nodeAffinity:
      requiredDuringSchedulingIgnoredDuringExecution:
        nodeSelectorTerms:
        - matchExpressions:
          - key: memSize
            operator: In
            values:
            - Large
          - key: memSize
            operator: NotIn
            values:
            - Small
```

