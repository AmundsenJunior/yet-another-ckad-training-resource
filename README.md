# yet-another-ckad-training-resource
The acronym is YACTR and it's pronounced yachter. **YACHTER**, y'all. Kept true to  the k8s nautical theme by sheer luck :satisfied:.

*Guides, links, commands, and YAMLs to help prepare for the Certified Kubernetes Application Developer (CKAD) exam*

## K8s and CKAD 

* [Kubernetes Docs](https://kubernetes.io/docs/home/)
* Linux Foundation, [The CKAD Exam](https://training.linuxfoundation.org/certification/certified-kubernetes-application-developer-ckad/)
* Cloud Native Computing Foundation, [The CKAD Exam](https://www.cncf.io/certification/ckad/)
  * [Exam Curriculum](https://github.com/cncf/curriculum/blob/master/CKAD_Curriculum_V1.14.1.pdf)
  * [Candidate Handbook](https://training.linuxfoundation.org/go/cka-ckad-candidate-handbook)
  * [Exam Tips](http://training.linuxfoundation.org/go//Important-Tips-CKA-CKAD)
  * [Exam FAQ](http://training.linuxfoundation.org/go/cka-ckad-faq)

## Main Training 

* [Udemy - CKAD training](https://www.udemy.com/certified-kubernetes-application-developer) from [Mumshad Mannambeth](https://twitter.com/mmumshad)
  * [My course notes](./Udemy-CKAD-Practice.md)
* Kim Wuestkamp on Codeburst, "[CKAD Weekly Challenge Overview](https://codeburst.io/kubernetes-ckad-weekly-challenges-overview-and-tips-7282b36a2681)"
  1. "[Creating Pods](https://medium.com/faun/kubernetes-ckad-weekly-challenge-1-creating-pods-a9510aab8978)"
  2. "[Namespaces, Deployments, and Services](https://medium.com/faun/kubernetes-ckad-weekly-challenge-2-namespaces-deployments-and-services-de1ede24679a)"
  3. "[CronJobs and Volumes](https://medium.com/faun/kubernetes-ckad-weekly-challenge-3-cronjobs-dbd400526673)"
  4. "[Deployment Rollout Rollback](https://medium.com/faun/kubernetes-ckad-weekly-challenge-4-deployment-rollout-rollback-aa251579ebaf)"
  5. "[Secrets and ConfigMaps](https://medium.com/faun/kubernetes-ckad-weekly-challenge-5-secrets-und-configmaps-550afde679fe)"
  6. "[NetworkPolicy](https://medium.com/faun/kubernetes-ckad-weekly-challenge-6-networkpolicy-6cc1d390f289)"
  7. "[Migrate a Service](https://codeburst.io/kubernetes-ckad-weekly-challenge-7-migrate-a-service-68c7af41c8df)"
  8. "[User Authorization RBAC](https://codeburst.io/kubernetes-ckad-weekly-challenge-8-user-authorization-rbac-31b6d01a8143)"
  9. "[Logging Sidecar](https://codeburst.io/kubernetes-ckad-weekly-challenge-9-logging-sidecar-67b2be91aa93)"
  10. "[Deployment Hacking](https://codeburst.io/kubernetes-ckad-weekly-challenge-10-deployment-hacking-fce74f41cad5)"

## CKAD Exam Prep and Testimony

Good resources for being prepared to take the exam:
* Kim Wuestkamp on Codeburst, "[The CKAD Browser Terminal](https://codeburst.io/the-ckad-browser-terminal-10fab2e8122e)"
* Haripraghash Subramaniam on Medium, "[CKAD - My Journey](https://medium.com/@harioverhere/ckad-certified-kubernetes-application-developer-my-journey-3afb0901014)"
* Atharva Chauthaiwale on Medium, "[My CKAD Exam Experience](https://medium.com/@atharvac.cloud/my-ckad-exam-experience-5e10c3640273)"
* GitHub [dgkanatsios/CKAD-exercises](https://github.com/dgkanatsios/CKAD-exercises)
* GitHub [lucassha/CKAD-resources](https://github.com/lucassha/CKAD-resources)
* GitHub [nikhilagrawal577/ckad-notes](https://github.com/nikhilagrawal577/ckad-notes)

## Additional K8s References and Training

Other training and review resources for k8s encountered (not CKAD-specific):
* [GitHub ramitsurana/awesome-kubernetes](https://github.com/ramitsurana/awesome-kubernetes)
* Atharva Chauthaiwale on Medium, "Kubernetes Deep Dive"
  1. "[Init Containers and Lifecycle Hooks](https://medium.com/@atharvac.cloud/kubernetes-deep-dive-part-1-init-containers-and-lifecycle-hooks-8da160b5cd4e)"
  2. "[Pod Presets](https://medium.com/@atharvac.cloud/kubernetes-deep-dive-part-2-pod-preset-635769296529)"
  3. "[Generators for Quick POCs](https://medium.com/@atharvac.cloud/kubernetes-deep-dive-part-3-generators-for-quick-poc-6cac698f08eb)"
* [IBM Kubernetes 101](https://github.com/IBM/kube101)
* [Kubernetes the Hard Way](https://github.com/kelseyhightower/kubernetes-the-hard-way), if you need to understand k8s under the hood, or want to get a jump-start on prepping for the Certified Kubernetes Administrator (CKA) exam
* *[Kubernetes Up and Running](http://shop.oreilly.com/product/0636920043874.do)* a comprehensive k8s development book from the k8s creators

## How to YAML

All k8s files adhere to the YAML spec:
* [The YAML spec](https://yaml.org/spec/1.2/spec.html)
* IBM - [YAML in K8s](https://developer.ibm.com/tutorials/yaml-basics-and-usage-in-kubernetes/)

## How to Vim

Working solely in a terminal during the exam, here are resources to learn how to use `vim` quickly and efficiently (`emacs` and `nano` are probably also allowed):
* Peter Jang on Medium, "[How to Learn Vim: A Four Week Plan](https://medium.com/actualize-network/how-to-learn-vim-a-four-week-plan-cd8b376a9b85)"
* Open Vim - [Interactive Vim Browser-based Tutorial](https://www.openvim.com/)
* `$ vimtutor` in your terminal

## How to tmux

According to the CKAD Candidate Handbook from CNCF (see link above), `tmux` and `screen` are allowed to provide multiple panes in your terminal window.
* Hackernoon, "[A Gentle Introduction to tmux](https://hackernoon.com/a-gentle-introduction-to-tmux-8d784c404340)"
* Peter Jang on Medium, "[A Minimalist Guide to tmux](https://medium.com/actualize-network/a-minimalist-guide-to-tmux-13675fb160fa)"
* Ham Vocke, "[A Quick and Easy Guide to tmux](https://www.hamvocke.com/blog/a-quick-and-easy-guide-to-tmux/)"