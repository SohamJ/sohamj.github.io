---
tags:
  - certification
  - kubernetes
  - exam
cards-deck: Technology::Kubernetes::Certified Kubernetes Application Developer
title: Certified Kubernetes Application Developer
date: 2025-06-18
description: Kubernetes CKAD exam preparation along with Kode Kloud/Udemy CKAD course notes
aliases:
  - CKAD
---
# Exam Resources

## Exam Topics
#card
> [!abstract]- Exam Topics
> 
> **Application Design and Build (20%)** 
> Define, build and modify container images  
> Choose and use the right workload resource (Deployment, DaemonSet, CronJob, etc.)  
> Understand multi-container Pod design patterns (e.g. sidecar, init and others)  
> Utilize persistent and ephemeral volumes
>
> **Application Deployment (20%)**  
> Use Kubernetes primitives to implement common deployment strategies (e.g. blue/green or canary)  
> Understand Deployments and how to perform rolling updates  
> Use the Helm package manager to deploy existing packages  
> Kustomize
>
> **Application Observability and Maintenance (15%)**
> Understand API deprecations  
> Implement probes and health checks  
> Use built-in CLI tools to monitor Kubernetes applications  
> Utilize container logs  
> Debugging in Kubernetes
>
> **Application Environment, Configuration and Security (25%)**
> Discover and use resources that extend Kubernetes (CRD, Operators)  
> Understand authentication, authorization and admission control  
> Understand Requests, limits, quotas  
> Understand ConfigMaps  
> Create & consume Secrets  
> Understand ServiceAccounts  
> Understand Application Security (SecurityContexts, Capabilities, etc.)
>
> **Services and Networking (20%)**
> Demonstrate basic understanding of NetworkPolicies  
> Provide and troubleshoot access to applications via services  
> Use Ingress rules to expose applications

<!--SR:!2025-05-21,4,280-->

### Additional Certification Information

* [Certification Info](https://trainingportal.linuxfoundation.org/courses/certified-kubernetes-application-developer-ckad)
* [Learning Path](https://training.linuxfoundation.org/wp-content/uploads/2024/10/CKAD_CurriculumPath.pdf?_gl=1*1lh86jf*_gcl_au*NjgxMTM0MTcwLjE3MzkwMzUyODE.*_ga*MTYzOTcxNTc0Ni4xNzM5MDM1Mjgx*_ga_EMX7DDZMX4*MTczOTAzNTI4MS4xLjEuMTczOTAzNTMzMS4xMC4wLjA.)
* [Youtube - Example questions](https://www.youtube.com/watch?v=wHha-Q3XVOg)
* [CKAD Important Instructions](https://docs.linuxfoundation.org/tc-docs/certification/tips-cka-and-ckad)
* [FAQs](https://docs.linuxfoundation.org/tc-docs/certification/faq-cka-ckad-cks)

## Test Exams

* [Practice on KillerCoda](http://killercoda.com/)
* https://github.com/dgkanatsios/CKAD-exercises

## Exam Pattern
#card
* The exam is 2 hours long and contains between 15–20 tasks. ~6 mins per question
* Each task is worth a certain percentage of the total grade, e.g. 4% or 8%. 
* The pass mark for the exam is 66%.
* No MCQs

## Exam Technical Requirements
#card
* Copy/Paste = Control + Shift + C / V
* `ssh <host>` for each question
* `ssh base` to get back
* cli tools -  `k`, `jq`, `tmux`, `curl`, `man`

## References Allowed During the Exam

* [List of Allowed References](https://docs.linuxfoundation.org/tc-docs/certification/certification-resources-allowed#certified-kubernetes-administrator-cka-and-certified-kubernetes-application-developer-ckad)
    * [API Reference](https://v1-31.docs.kubernetes.io/docs/reference/generated/kubernetes-api/v1.31/)
    * [Helm]([https://helm.sh/docs](https://helm.sh/docs))

## Linux Foundation Exam Platform

* [Scheduling Exam](https://docs.linuxfoundation.org/tc-docs/certification/lf-handbook2/scheduling-or-rescheduling-an-exam)
* [Certification Policy]([https://training.linuxfoundation.org/certification-policy-change-2024/](https://training.linuxfoundation.org/certification-policy-change-2024/))
* [Exam System Requirements](https://docs.linuxfoundation.org/tc-docs/certification/lf-handbook2/candidate-requirements)


## Tips
#card 

### Summary

> [!SUMMARY] Personal Tips
> 
> * Do the practice tests. We get two tries. I would suggest to take both even though the questions are the same (for CKAD). This will help you get used to the PSI interface. The exam interface is slightly worse than the practice exams, especially when it comes to copying text from the question to the terminal window and overall network performance since your webcam is always on which consumes the bandwidth
> * The PSI interface has a white top menu bar which takes up quite some space. Minimize this bar to get as much screen real estate as you can. I was comfortable using my laptop screen 15". If you have a smaller laptop (13/14") then I would suggest using an external monitor
> * Always SSH into the node before starting the question and exit after completing the question
> * Skim through the question to find which namespace is to be used
> * Set `alias k=kubectl -n <namespace>`. Remember to run `helm` commands with the namespace flag, or set an alias for that question using `alias helm=helm -n <namespace>`. I did not use `k config set-context` 
> * Check if the question mentions any existing YAML resource files or Dockerfiles. If it does, make a copy of the original before starting to make any edits
> * When you edit the file using vi, type `:set ai` to auto-indent code. Learn how to use visual mode (`V`) and `>` to indent blocks of lines that you may copy from existing YAML resources or from the docs. You won't have enough time to configure `vimrc` on each node
>     * Refer: [Vim Keybindings](https://vim.rtorr.com/)
> * If you don't have a general idea on how to solve the question after reading through it, flag the question and go to the next one
> * Generate YAML resources using `kubectl create` command. Make sure you remember the list resources it supports (`--help` flag is always there to help!)
>     * For resources that need slight modifications that the `kubectl create` does not support (e.g. creating a `NodePort` [[Kubernetes Service]]), use `k --dry-run=client -o yaml` to generate the YAML resource as a starting point
>     * For resources not supported by the imperative command (e.g. `NetworkPolicy`, `PersistentVolume`, `CustomResourceDefinition`s), copy the example YAMLs from the Kubernetes doc site
> * I used VS Codium as a clipboard to copy common commands such as `kubectl run --rm -it nginx -- <command>` for questions related to network troubleshooting. Alternatively, you can use `Control + R` to search your shell history
> * Use `kubectl explain` for finding information about specific resource fields. Two hours is not enough time to go to the documentation site and read through the resource specifications
> * Make sure there are no typos in resource names and metadata fields. You can take an extra second to verify these values
> * Always delete resources using `--force`. I didn't have to include `--grace-period=0`
> * `kubectl expain` can get a bit verbose for certain fields such as `pod.spec.volumes`. Use `k explain pod.spec.volumes --recursive` in such cases
> * Don't forget to use `k get -o wide`. It is especially useful when dealing with services and nodes
 
#### Some Gotchas to Remember
 
* [[Kubernetes Network Policies]]: set the ingress/egress rule port to the container port, not service port
* [[Kubernetes Pod]]: Learn how to use `kubectl get po -L` to filter pods by label selectors
* [[Kubernetes Service]]: Double-check if service needs to have a specific name. It will default to the pod name if created using the `kubectl expose` command. Remember that `kubectl create` command does not create a NodePort service
* [[Kubernetes Pod]]: Sidecar containers should be created as a initContainers with `RestartPolicy`: Always
* [[Helm]]: `helm show` is to see chart details. `helm search` is to find charts and versions. Internalize this to avoid confusion during the exam
* [[Helm]]: `helm -a` is to find pending releases, `helm -A` is all namespaces
* [[Kubernetes Secret]]/[[Kubernetes ConfigMap]]: Go through the question to understand how secrets/configmaps need to be used - read specific keys as env variables using `valueFrom` vs fetching all keys using `envFrom` vs mounting configs as files
* [[Kubernetes Deployment]]: for blue-green or canary deployments, make sure both deployments have unique labels (e.g. `version=v1` and `version=v2`) but pod labels are the same (e.g. `app=frontend`). Service has to point to pods in both deployments using the pod labels

### Tips from Linux Foundation Site
#### Knowledge

- Study all topics as proposed in the curriculum till you feel comfortable with all
- Learn and Study the in-browser scenarios on [https://killercoda.com/killer-shell-ckad](https://killercoda.com/killer-shell-ckad)
- Read this and do all examples: [https://kubernetes.io/docs/concepts/cluster-administration/logging](https://kubernetes.io/docs/concepts/cluster-administration/logging)
- Understand Rolling Update Deployment including `maxSurge` and `maxUnavailable`
- Do 1 or 2 test session with this CKAD Simulator. Understand the solutions and maybe try out other ways to achieve the same
- Be fast and breath `kubectl`

#### CKAD Preparation

* Read the Curriculum: [https://github.com/cncf/curriculum](https://github.com/cncf/curriculum)
* Read the Handbook: [https://docs.linuxfoundation.org/tc-docs/certification/lf-handbook2](https://docs.linuxfoundation.org/tc-docs/certification/lf-handbook2)
* Read the important tips: [https://docs.linuxfoundation.org/tc-docs/certification/tips-cka-and-ckad](https://docs.linuxfoundation.org/tc-docs/certification/tips-cka-and-ckad)
* Read the FAQ: [https://docs.linuxfoundation.org/tc-docs/certification/faq-cka-ckad](https://docs.linuxfoundation.org/tc-docs/certification/faq-cka-ckad)

#### Kubernetes documentation

Get familiar with the Kubernetes documentation and be able to use the search. Allowed resources are:
- [https://kubernetes.io/docs](https://kubernetes.io/docs)
- [https://kubernetes.io/blog](https://kubernetes.io/blog)
- [https://helm.sh/docs](https://helm.sh/docs)

> ℹ️ Verify the list [here](https://docs.linuxfoundation.org/tc-docs/certification/certification-resources-allowed)

#### The Exam UI / Remote Desktop

The real exam, as well as the simulator, provides a Remote Desktop (XFCE) on Ubuntu/Debian. Coming from OSX/Windows there will be changes in copy & paste for example.

**Official Information**

[ExamUI: Performance Based Exams](https://docs.linuxfoundation.org/tc-docs/certification/lf-handbook2/exam-user-interface/examui-performance-based-exams)

**Lagging**

There could be some lagging, definitely make sure you are using a good internet connection because your webcam and screen are transferring all the time.

**Kubectl autocompletion and commands**

The following are installed or pre-configured, verify the list [here](https://docs.linuxfoundation.org/tc-docs/certification/tips-cka-and-ckad):

- `kubectl` with `k` alias and Bash autocompletion
- `yq` or YAML processing
- `curl` and `wget` for testing web services
- `man` and man pages for further documentation

> ℹ️ You're allowed to install tools, like `tmux` for terminal multiplexing or `jq` for JSON processing

**Copy & Paste**

Copy and pasting will work like normal in a Linux Environment:

What always works: copy+paste using right mouse context menu What works in Terminal: Ctrl+Shift+c and Ctrl+Shift+v What works in other apps like Firefox: Ctrl+c and Ctrl+v

**Score**

There are 15-20 questions in the exam. Your results will be automatically checked according to the handbook. If you don't agree with the results you can request a review by contacting the Linux Foundation Support.

**Notepad & Flagging Questions**

You can flag questions to return to later. This is just a marker for yourself and won't affect scoring. You also have access to a simple notepad in the browser which can be used to store any kind of plain text. It might make sense to use this and write down additional information about flagged questions. Instead of using the notepad you could also open Mousepad (XFCE application inside the Remote Desktop) or create a file with Vim.

**VSCodium**

You can use VSCodium to edit files and you can also use its terminal to run commands. You're not allowed to install any VSCodium extensions.

**Servers**

Each question needs to be solved on a specific instance other than your main terminal. You'll need to connect to the correct instance via ssh, the command is provided before each question.

### PSI Bridge

Starting with [PSI Bridge](https://training.linuxfoundation.org/bridge-migration-2021):

- The exam will now be taken using the PSI Secure Browser, which can be downloaded using the newest versions of Microsoft Edge, Safari, Chrome, or Firefox
- Multiple monitors will no longer be permitted
- Use of personal bookmarks will no longer be permitted

The new ExamUI includes improved features such as:
- A remote desktop configured with the tools and software needed to complete the tasks
- A timer that displays the actual time remaining (in minutes) and provides an alert with 30, 15, or 5 minute remaining
- The content panel remains the same (presented on the Left Hand Side of the ExamUI)

Read more [here](https://training.linuxfoundation.org/bridge-migration-2021).

### Terminal Handling

#### Bash Aliases

In the real exam, each question has to be solved on a different instance to which you connect via ssh. This means it's not advised to configure bash aliases because they wouldn't be available on the instances accessed by ssh. (**I disagree - using `alias k=kubectl -n namespace` helps a lot!**)

#### Be fast

Use the `history` command to reuse already entered commands or use even faster history search through **Ctrl r**
If a command takes some time to execute, like sometimes `kubectl delete pod x`. You can put a task in the background using **Ctrl z** and pull it back into foreground running command `fg`.

You can delete _pods_ fast with:

`k delete pod x --grace-period 0 --force`

#### Vim

Be great with vim

**Settings**

In case you face a situation where vim is not configured properly and you face for example issues with pasting copied content you should be able to configure via `~/.vimrc` or by entering manually in vim settings mode:
```
set tabstop=2
set expandtab
set shiftwidth=2
```
The `expandtab` make sure to use spaces for tabs.

Note that changes in `~/.vimrc` will not be transferred when connecting to other instances via ssh.

**Toggle vim line numbers**

When in `vim` you can press **Esc** and type `:set number` or `:set nonumber` followed by **Enter** to toggle line numbers. This can be useful when finding syntax errors based on line - but can be bad when wanting to mark & copy by mouse. You can also just jump to a line number with **Esc** `:22` + **Enter**.

**Copy & Paste**

* Get used to copy/paste/cut with vim:
* Mark lines: Esc+V (then arrow keys)
* Copy marked lines: y
* Cut marked lines: d
* Past lines: p or P
* **Indent multiple lines**
  * To indent multiple lines press **Esc** and type `:set shiftwidth=2`. 
  * First mark multiple lines using `Shift v` and the up/down keys. Then to indent the marked lines press `>` or `<`. You can then press `.` to repeat the action.

### Tips from Other Students
#card
* [Medium - prep guide](https://medium.com/@michael_england/how-i-passed-the-certified-kubernetes-application-developer-ckad-exam-cd443f160643)
    * Set correct context with namespace every time `k config set-context --current --namespace <namespace>`
    * Use bigger monitor
    * Create files with question number as the prefix
    * Use `k explain`
* [CKAD Experience](https://www.linkedin.com/pulse/my-ckad-exam-experience-atharva-chauthaiwale)
    * Use aliases for `k --namespace <ns>` and `k run .. --dry-run=client -o yaml` and vim options for editing
    ```shell
    export ns=default
    alias k='kubectl -n $ns' # This helps when namespace in question doesn't have a friendly name
    alias kdr= 'kubectl -n $ns -o yaml --dry-run'.  # run commands in dry run mode and generate yaml.
    ```
    ```shell
    vim ~/.vimrc
    set nu
    set expandtab
    set autoindent
    set shiftwidth=2
    set tabstop=2
    ```
<!--SR:!2025-06-06,8,272-->
    
* [Medium - my CKAD journey](https://medium.com/@harioverhere/ckad-certified-kubernetes-application-developer-my-journey-3afb0901014)
    * Answer questions by weightage (not sequentially)
* [Github - lucassha CKAD resources](https://github.com/lucassha/CKAD-resources)
    * Create resource template files ahead of time
    * use `head` to find examples from `kubectl --help` command

# Course


> [!info] KodeKloud Community
> * https://kodekloud.com/pages/community/

## Section 1 - Introduction

### Kubernetes Architecture
#card
* Cluster has multiple Node - workers
* [[Kubernetes API Server]] - access APIs. Runs on the master node
* [[etcd]] - stores all configurations. Runs on the master node
* [[Kubernetes Scheduler]] - assigns workloads. Runs on the master node
* controller - manage workloads. Runs on the master node
* [[kubelet]] - runs on each node to check all workloads on a node
<!--SR:!2025-05-21,4,280-->

### Docker vs ContainerD
#card
* OCI has a imagespec and a runtimespec
* Docker used to use dockershim not CRI. [[containerd]] and crio are now used as runtimes
* `crictl` can be used to interact with all CRI runtimes. `containerd` comes with `ctr` cli and `nerdctl` for docker like commands to run containers
<!--SR:!2025-06-02,16,290-->

## Section 2 - Core Concepts

### [[Kubernetes Pod]]s
#card
* Smallest object in Kubernetes
* Contains one or more pod (helpers). Scale pods on multiple nodes
* `k run mypod -it --image nginx -- sh`
* YAML always has `apiVersion`, `kind`, `metadata`, `spec`
* `metadata` needs to have a `name`. In addition, `labels`, `annotations`
* Use `k get po -o wide` to see the nodes
* Total number of containers are under the `READY` column of the `k get po` command
* `k edit` command allows specific spec changes. Use the yaml file to edit
* When we set a `command`, use `sh -c` and then pass the command
<!--SR:!2025-06-01,15,290-->

### [[Kubernetes ReplicaSet]]s
#card
* Scale up and manage the expected number of controllers
* We pass the pod template in the `spec.template` section
* Requires `spec.selector` to map a [[Kubernetes ReplicaSet]] to pod template. It can manage pods outside the template spec as well
* To increase the replicas, we can update the yaml resource, or use `k scale --replicas=<new-count>`
* To delete all pods in a replicaset use the label -  `k delete po -l key=value` 

### [[Kubernetes Deployment]]
#card
* Manage rollouts of replicaset-managed pods
* `k get all` will show deployment, replicaset, and pods
* `k create deployment <deployment> --image <foo> --dry-run=client -o yaml > deployment.yaml` 

### [[Kubernetes Service]]
#card
* Communicate to other pods in the cluster
* Creates a DNS with the name of the service
* Use `k expose pod <pod> --port=<port> --name <service-name> --dry-run=client -o yaml` to create a service for a pod
* `k create svc clusterip <service-name> --tcp=<port>:<port> --dry-run=client -o yaml` is also an option, but this defaults to the selector `app=<service-name>
* Can create a service while creating the pod using `k run po .. --expose=true  --port=1234`

### [[Kubernetes Namespace]]
#card
* Analogy - two different houses. Refer to a person in another house using first and last name. Refer to person in the same house with first name only
* Isolated tenants in Kubernetes cluster
* Allocate quota
* Use service DNS - `<service>.<namespace>.svc.cluster.local`
* `k config set-context $(kubectl config current-context --namespace=<namespace>` to switch namespace in the same context
* `kubectl -A` checks all namespaces 
### Labels and Selectors
#card
* Labels allow to filter workloads and selectors map different resources together using those labels
* We can filter resources like pods using `k get po -l key=value`, or see labels on all pods using `k get po --show-labels`

## Section 3 - Configuration

### Docker Container Arguments
#card
* Containers run as long as the process mentioned in `ENTRYPOINT` and/or `CMD` lives
* `CMD` is used as an argument to the `ENTRYPOINT`

### Kubernetes Arguments
#card
* We set `command` for entrypoint and `args` for cmd in [[Kubernetes Pod]] template
* We cannot edit pod template except `image`, `activeDeadlineSeconds` and `tolerations` fields
* `kubectl edit` of any other field will fail and save a temp file which we can apply to create another pod if needed
* `command` and `args` are string arrays
<!--SR:!2025-05-21,4,291-->

### Kubernetes Environment, [[Kubernetes ConfigMap]]s, and Secrets
#card
* Use `env` array of key-value maps to set environments
* Use `envFrom` array to fetch the [[Kubernetes ConfigMap]] data. Use `env.valueFrom.configMapKeyRef` to get value of an env variable from the `ConfigMap`
* Use `k create cm <name> --from-literal` to create `ConfigMap` manually
* secrets are base64 encoded (`echo -n <value> | base64`)
* Each attribute in a secret is mounted as a file in the pod
* [[kubelet]] stores secrets in TMPFS on the node, not the filesystem. It also only pulls it if a pod requests a secret

#### Encrypting Kubernetes Secrets at Rest
#card
* We can use `etcdctl` to encrypt etcd
* A `EncyptionConfiguration` resource is used to enable encryption. That is then set on the api server
* Existing secrets aren't encrypted unless we explicitly replace it
<!--SR:!2025-05-31,14,290-->

### Docker Security

* Containers are namespace-d
* Root user in the container doesn't have root access on the host, but it can get some specific privileges (`--cap-add` or `--privileged`)

### Kubernetes Security Contexts
#card
* Kubernetes allows security configurations on pod-level or container using `securityContext` section
* Get user running the pod - `k exec -it <pod> -- whoami`

### [[Kubernetes ServiceAccount]]s
#card
* Authentication to talk to the [[Kubernetes API Server]]. Serviceaccount has a Bearer token stored as a Kubernetes secret
* Associated with the [[Role-Based Access Control]] configurations to grant permissions to [[Kubernetes API Server]]
* Each namespace has a `default` serviceaccount
* [[Kubernetes ServiceAccount]] is mounted in the pod under `/var/run/secrets/kubernetes.io/serviceaccount` (not default in newer versions). `automountServiceaccountToken: true`
* Tokens are bounded and have a expiration time since 1.22. These temporary tokens are mounted in the pod using `TokenRequest` API made
* 1.24 also removed the token secret in the [[Kubernetes ServiceAccount]]. We need to create a secret and map it to a serviceaccount using an annotation

### Kubernetes Resource Requirements
#card
* [[Kubernetes Scheduler]] decides how to place the pod on a node based on the requested resources. It uses the `requests`, not `limits` to schedule
* 1 cpu == 1 virtual CPU.
* Each container can have its own resource limits. Defaults are unbounded
* Container can use more memory than the limit but can get OOM
* requests default to limits if not set
* [[LimitRange]] allows to default per-pod requests and limits on a namespace level. [[ResourceQuota]] limits total namespace resources
<!--SR:!2025-06-01,15,290-->

### [[Kubernetes Taints and Tolerations]]
#card
* Restrict pod scheduling by setting a taint on the node and set a toleration that will align with the taint. The pod has to "tolerate" the taint on the node
* Taint effects - `NoSchedule` won't schedule new pods. `PreferNoSchedule` will try not to schedule new pods. `NoExecute` = NoSchedule + evict all existing pods that are not tolerated
* `k taint nodes <node> <key>=<value>:<effect>`. A `-` at the end will remove the taint

### [[Kubernetes Node Selectors]] and [[Kubernetes Node Affinity]]
#card
* Nodes are labeled and node selector uses the label
* `k label node <node> key=value`
* Node Affinity is more flexible by providing match expressions -- e.g. key *In* value, key *NotIn* value, key *Exists*. Is it required or preferred during scheduling or execution?
    * `requiredDuringScheduling` vs `preferredDuringScheduling`. Currently Kubernetes only supports `IgnoredDuringExecution` to not evict currently running nodes
* Combine [[Kubernetes Node Affinity]] to map a pod to a node and use [[Kubernetes Taints and Tolerations]] to repel other pods from those nodes
<!--SR:!2025-05-31,14,290-->

## Section 4 - Multi-Container Pods

### Multi-Container Pods
#card
* Allows decoupling of services but follow the same lifecycle, storage, networks
* Patterns - sidecar (e.g. logging agent), adapter (e.g. convert different logs into json), ambassador (e.g. act as a proxy for environment specific configurations like database urls)
* Use `k replace --force -f` to replace a pod with a pod + sidecar
* sidecars should be created as [initContainers](#init-containers) with a `restartPolicy: Always` instead of adding them in the `containers` section which is now a legacy approach

### Init Containers
#card
* Run before the main containers and go away after completion
* Defined under `initContainers` section
* Init containers run serially
<!--SR:!2025-05-21,4,292-->

## Section 5 - Observability

### Readiness and Liveness Probes
#card 
* Pod Status - where the pod is in its lifecycle. Pending (to be scheduled) --> ContainerCreating (pull images) --> Running
    * `k get pod` shows the pod status
* Pod Condition - Additional Boolean information about the status
    * `PodScheduled`, `Initialized`, `ContainersReady`, `Ready` (ready also shows in `k get pod`)
* Application may take a while to start once the container is started. [[Kubernetes Service]] will route traffic as soon as the pod is ready but may get failures since the application has not started yet
* [[Readiness Probe]] (`readinessProbe`) makes sure to set the `Ready` condition only until the condition of the probe is satisfied
* [[Liveness Probe]] (`livenessProbe`) periodically checks whether the container is healthy and restarts the pod
* Probe can be `httpGet`, `tcpSocket.port`, or `exec.command`
* Probes can have an `initialDelaySeconds`, can have a `failureThreshold` and a frequency set using `periodSeconds`

### Container Logging
#card
* Use `kubectl logs -f` command. Additionally a `-c <container>` flag for a specific container
<!--SR:!2025-05-31,14,290-->

### Monitoring Kubernetes Cluster
#card
* Kubernetes has a inbuilt Metrics Server which maintains information in-memory
* [[kubelet]] stores the information using `cAdvisor`
* `kubectl top pod|node` shows the metrics
<!--SR:!2025-05-21,4,280-->


## Section 6 - Pod Design

### Labels, Selectors, and Annotations
#card
* Labels and selectors group objects together and allow classification/filtering
* Selectors map a [[Kubernetes ReplicaSet]] to [[Kubernetes Pod]]s, or a [[Kubernetes Service]] to [[Kubernetes Pod]]s
* `k get po -l <key1>=<value1>,<key2>=<value2>[...]` is used to filter by label
* Use `k get po --no-headers | wc` to count number of pods
<!--SR:!2025-06-02,16,290-->

### [[Kubernetes Deployment]] Rolling Updates and Rollbacks
#card
* `k rollout status deploy <deployment>` checks the deployment status and `k rollout history` shows previous updates
* Deployment strategy - `Recreate` removes existing pods and creates new one. This can cause downtime. Rolling Update brings up new pods then scales down previous ones (with different weight but defaulting to 25% max unavailability and 25% surge)
* `--record` flag helps capture the change cause in the rollout history. This flag was deprecated in newer Kubernetes version
* `k rollout undo` with an optional `--to-revision` will rollback to a specific revision
* `k set image <deploy/<deployment> <container-name>:<image>` updates the image
<!--SR:!2025-06-09,11,292-->

### Blue-Green Deployments
#card 
* We stand up 2 versions of the pod. The traffic goes to the original version. Once the new version is tested, we route traffic to the new version

### Canary Deployments
#card
* We stand up new version and route small percentage of traffic to the new version while continuing to send traffic to original version
* Poor man's canary would be to scale the pods in the new version to scale traffic. [[Istio]] or similar services allow granular control
<!--SR:!2025-06-01,15,290-->

### [[Kubernetes Job]]s [[Kubernetes CronJob]]s
#card 
* [[Kubernetes Pod]]s are configured to always restart after they complete and crash
* Jobs allow batch or event driven workloads to run to completion
* Specify how many runs are required for successful execution using `completions`. The pods spin up serially. We can set `parallelism` to run them in parallel
* Same as [[Kubernetes Job]], [[Kubernetes CronJob]] adds a `cron` schedule
* Use `watch kubectl get job` to see the completions count
* The cron `schedule` follows the syntax `<min 0-60/interval> <hour 0-24/interval> <date 1-31/interval> <month 1-12/interval> <day of month 1-7/interval>

## Section 7 - Services and Networking

### Kubernetes Services
#network #card
* [[Kubernetes Service]] allows connection between pods. This service type is `ClusterIP`
* A `NodePort` service exposes a pod on the node level using a port on the node. `nodePort` -> Service Port -> Pod container's port  (`TargetPort`). Service can expose a `nodePort` on multiple nodes where the pods are running
* Another type of service is `LoadBalancer`. Kubernetes creates a nodePort service and also creates a load balancer in the cloud to expose the service
* A `selector` maps the service to the pod(s). The pods mapped to the service are recorded as [[Kubernetes Endpoint]]s. It is possible other pods that were already deployed match the selector. This is why endpoint resource is used instead of mapping the pod IPs on the service directly

### Cluster IP Service
#card
* Since pods have dynamic IPs, we need a service to group and access the pods
* We can access the pods using the cluster IP or the service name

### [[Kubernetes Ingress]]
#network #card
* We can use `LoadBalancer` service to expose traffic outside the cluster. However, we need to create new load balancers for each application. The load balancers would have the `nodePort`s in the ranges of 30000+ which we will need to remember. Another proxy layer can be introduced on top to manage them
* However, to manage configurations such as path based routing, SSL, and other HTTP ([[Layer7]]) configs on the Kubernetes layer, we can instead use Ingress
* Kubernetes doesn't have Ingress controller built in. We can deploy [[NGINX]], [[HAProxy]], [[Istio]] or similar [[Reverse Proxy]] tools
* Ingress maps to a [[Kubernetes Service]] using its name and port
* Ingress supports multiple rules to route traffic to different hosts and paths. If `rules.host` is not defined, the `rules.http.paths` rules map all hosts to a `backend` at a particular `path`
* Ingress uses a `defaultBackend` to route traffic that don't match the rules. That can be customized to provide custom 404 messages
* `k create ingress <NAME> -n <NAMESPACE> --rule="[HOST]/PATH=SERVICE:PORT"`
* `nginx.ingress.kubernetes.io/rewrite-target` annotation allows rewriting the path passed on the ingress to the backend. E.g. ingress will accept traffic on `/foo` but the app only serves traffic on `/` so we replace `/foo` with `/` using `rewrite-target: /`
* There can be regex rules with a capture group such as `path: /something(/|$)(.*)` rewritten to the 2nd capture group using `rewrite-target: $2`
* We need to set the `ingressClassName` to register the ingress against an IP

### [[Kubernetes Network Policies]]
#network #card 
* By default, all pods can talk to each other
* `NetworkPolicy` allows strict ingress and egress traffic rule types. To block something, we have to explicitly define the ingress/egress rule
* We define `ingress.from` rule and/or `egress.to` rule and use a pod and optional namespace selector to specify the source/destination or even an `ipBlock`. Multiple rules are `OR`'d 
* For egress rules, we sometimes need to allow all DNS traffic. In that case, the `egress.to` block can be empty and only ports can be defined:
    ```yaml
      egress:
      # NO - to: 
        ports:
        - protocol: TCP
          port: 53
        - protocol: UDP
          port: 53
    ```

## Section 8 - State Persistence

### Container Volumes
#card
* Containers are transient, so volumes are used to persist data
* Kubernetes uses a list of `volumes` which define the path to mount to and `volumeMounts` to define where to mount the volume from
* `volume` type can range from `hostPath` to different drivers like `awsEbsBlockStore`
* [[Kubernetes Persistent Volumes]] expose the volume configuration out of the [[Kubernetes Pod]] spec to be used by one or more pod
* [[Kubernetes Persistent Volumes]] are created using [[Kubernetes Persistent Volume Claims]]
* [[Kubernetes Persistent Volumes]] have different `accessModes` - `ReadOnlyMany`, `ReadWriteOnce`, `ReadWriteMany`
* PVC binds a PV based on the properties defined on it - e.g. requested storage resources. Once the volume is bound to a PVC, no other PVC can claim it
* Once PVC is deleted, the PV can be deleted, retained or recycled (scrubbed)
* Once a PVC is created, it is defined under the Kubernetes pod or other controller's `volume` section
* A PV is `Available` upon creation. PVC goes into a `Pending` state until it finds the PV and then goes in a `Bound` state. PV also goes in a `Bound` state
* A PV won't be deleted and stays in a `Terminating` state until its not used. Once a PVC is deleted, the PV goes in a `Released` state
<!--SR:!2025-06-10,12,292-->

### StorageClass
#storage #card
* [[Kubernetes StorageClass]] automates the creation of a volume when a PVC is created. This is dynamic provisioning using a specific provisioner
* We don't have to manually create a [[Kubernetes Persistent Volumes]] anymore. StorageClass will create it
* `volumeBindingMode` allows the PVC to be bound immediately upon creation or wait until a pod uses it

### StatefulSets
#card
* [[Kubernetes StatefulSet]] provide a specific name to each pod unlike [[Kubernetes Deployment]]s
* They are also created in a sequential order from index 0. For databases, master is always the 1st pod
* It also creates its own headless service for inter-pod communication. This service only creates a DNS entry for each pod. It does not load balance or expose its own IP. (`clusterIP: None`)
* Pods within StatefulSet can have its own unique volume using `volumeClaimTempaltes`

## Section 9 - Security

### Authentication and Authorization
#authorization #authorization #card 
* [[Kubernetes API Server]] security is critical -- who can authenticate and what they are authorized to do
* Internal communication is secured through TLS certificates
* Users and service accounts are two main account types. Users are managed through external identity services (LDAP, Kerberos, etc)
* We can use basic authentication, tokens (bearer authentication) (deprecated in Kubernetes 1.19), TLS certificates
* The [[KubeConfig]] file stores the configuration to point to different clusters with different users. It maintains contexts to map a user to a cluster
* Using `k config` command to view, update, set context. context can be namespace specific as well
* Custom [[KubeConfig]] file can be passed using `k config --kubeconfig` or exporting `KUBECONFIG` environment variable

### API Groups
#api #card
* Core group under `/api` includes all main object types - namespaces, pods, rc, nodes, etc
* Named-groups under `/apis` are specific to each domain like networking, storage, extensions etc with multiple resources (e.g. replicaset, networkpolicies) and each API has different verbs (get, watch, delete, etc)

### Authorization
#authorization #authentication #card
* [[kubelet]] also accesses [[Kubernetes API Server]]. That is managed through Node Authorizer
* Attribute-based Access Control (ABAC) - maps user to a resource using policy
* [[Role-Based Access Control]] (RBAC) - maps users to a role. The role defines what access is allowed
* Webhooks to external systems like [[Open Policy Agent]] is also allowed
* In a [[Kubernetes Role]], `apiGroups: [""]` is used for the core group. `resourceNames` allow restricting to specific resources for a particular resource (e.g. pod)
* [[Kubernetes RoleBinding]] maps a role to subjects (users, groups, serviceaccount)
* `k auth can-i` command allows us to check the permissions
* `k create` command supports creation of role and rolebinding
* [[Kubernetes ClusterRole]] and [[Kubernetes ClusterRoleBinding]] are scoped on the cluster level
* To check if a resource is namespace-d, use `k api-resources --namespaced=true`

### Admission Controllers
#card
* [[Kubernetes Admission Controller]] go beyond RBAC resources which map subjects to [[Kubernetes API Server]] resources. They can check additional configurations or automatically modify API requests to adhere to specific configurations
* Built-in admission controllers - e.g. `NamespaceLifecycle` to check existing namespace, `DefaultStorageClass` to default a storage class
* `kubectl exec -it kube-apiserver-controlplane -n kube-system -- kube-apiserver -h | grep 'enable-admission-plugins'` shows the list of enabled admission controllers
* We can also check them on the running process on the node

### Validating and Mutating Admission Controllers
#card
* Validating Admission Controller checks whether something is allowed or not (e.g. NamespaceExists). Mutating Admission Controller updates the API data before its executed (e.g. NamespaceAutoProvision)
* Custom controllers can be set up using a webhook and a custom webhook server handling some logic
* Mutating webhooks run first before passing to the validating webhooks

### API Versions and Deprecations
#api #card
* `v1` - general stable version. Goes through `v1alpha1/2/..` (not enabled by default) -> `v1beta1/2..` -> `v1` -> `v2alpha/beta1/2/..` 
* Each resource can have multiple api versions but one is preferred storage version to be stored in etcd. The api version deprecation policy requires apis to support all resources until a new api version. Beta and GA api versions need to be supported for months/multiple releases. Only a new GA version can deprecate the old GA version
* `k convert` (plugin) command updates manifests

### Custom Resource Definition
#card
* [[Kubernetes Custom Resource Definition]] allows us to extend Kubernetes resources. CRD defines the name of the custom resource, what versions it supports, and the schema
* We create a custom controller (process) that will monitor [[Kubernetes API Server]] for CRD operations
* Kubernetes has a custom controller GitHub repository
* CRD and controllers are packaged into a operator

# Section 10 - Helm Fundamentals
#helm #card
* [[Kubernetes]] has multiple resources that are deployed as part of a typical application. [[Helm]] bundles all resources into a [[Helm Chart]] and supports templates to only pass the required configurations for your app while hardcoding others
* A `values.yaml` file stores all the variable values to be passed to a [[Helm Chart]]. The templates and a default values file is stored in the [[Helm Chart]]
* Each installation of a [[Helm Chart]] is called a [[Helm Release]]. Installation is using `helm install <release-name> <repo/chart>`
* The template placeholders use a [[Go Template]] like `{{ .Values.myValue }}` where a `values` file defines a property `myValue`
* Search helm chart info using `helm search repo <chart> --versions`
* Use `helm show values <chart>` to see chart values

# Section 11 - Kustomize

### Kustomize Basics
#card
* Common configurations for an app across environments can be abstracted into a common file. Parts of the file can be overridden if required
* There's a `base` configuration in the base directory for the common configurations and an `overlay` configuration in `overlays` directory to override the configurations
* There's no templating system like [[Helm]]. Helm supports [[Go Template]]s for conditional logic, functions and templating. [[Kustomize]] is simpler
* The [[Kustomize]] CLI looks for a `kustomization.yaml` file where we define all resources we want to manage and define different customizations or *transformations* we want to apply on them
* `kustomize build <directory>` spits out the generated [[Kubernetes]] resources which can be redirected to `kubectl apply -f -` to actually apply the resources or directly run `kubectl apply -k <directory>`
* Each `kustomization.yaml` file can optionally include `kind: Kustomize` and `apiVersion: kustomize.config.k8s.io/v1beta1` fields
* With multiple directories, we define a `kustomization.yaml` at the root of the directories and define all resource files in each subdirectory. We can also define a `kustomization.yaml` file in each subdirectory and the top file only defines the folders, not each file

### Kustomize Transformers
#card
* There are default *Common Transformers* like `commonLabels`, `commonAnnotations`, `Namespace`, `namePrefix`, `nameSuffix`, `secretGenerator`
* *Image Transformer* `images` allows specifying a name of the image in resources and replace that with an actual image and/or tag reference using `newName` and `newTag`.
* Example:
    ```yaml
    apiVersion: kustomize.config.k8s.io/v1beta1
    kind: Kustomization
    resources:
    - deploy.yaml
    images:
    - name: nginx
      newName: nginx
      newTag: 1.14.2
    
    commonLabels:
      description: 'nginx common label'
    
    namespace: my-namespace
    
    namePrefix: my-
    ```
<!--SR:!2025-05-21,4,292-->

### Kubernetes Patches
#card 
* Patches under `patches` allow changes to specific resources using `add`, `replace`, and `remove` operations on a `target`
    ```yaml
    patches:
      # provide one of more rules for a target
      - target:
        kind: Deployment
        name: api-deployment
    
        # define the patch inline
        patch: |-
        - op: replace
          path: /metadata/name
          value: web-deployment
    
        # a path can also be provided for a patch
        path: my-patch.yaml

      - target:
            kind: Deployment
            name: nginx
        patch: |-
          - op: add
            path: /metadata/labels/patch-label
            value: 'nginx patched label'
          - op: replace
            path: /metadata/labels/description
            value: 'nginx patched labelo'
      - target:
          kind: Deployment
          name: nginx
        patch: |-
          apiVersion: apps/v1
          kind: Deployment
          metadata:
            name: nginx
          spec:
            containers:
              - name: nginx
                image: nginx:1.14.2
                resources:
                  requests:
                    cpu: 100m
                    memory: 128Mi
    ```
* Patch can be of type `Json 6902` (above) or a *Strategic Merge Patch* to merge the original yaml with the patch. The patch should tell which resource to update and what values to update
    * To delete a key with a strategic patch, we set the value to null
* The patch can be defined separately using a `patches[].path`
* The patch `path` supports array index like `spec/template/spec/containers/0` to replace or delete or to add, we can do `/-` to add at the end of the list
    * To delete with *Strategic Merge Patch*, we define a `$patch: delete` and `name` property to delete a configuration

### Kustomize Overlays
#card
* In the `kustomization.yaml` file of an [[Kustomize Overlay]] directory, we define `bases` to the relate path of the base directory
* We can also define new resources
```yaml
bases:
  - ../../base

resources:
  - my-new-resource.yaml
```

### Kustomize Components
#card
* [[Kustomize Components]] are all reusable resources/patches that need to be applied to a **subset of overlays** instead of applying all through base
* Components are stored in its own folder `components`, like `base` or `overlays`  which is imported under the `components` property of `kustomization.yaml` file
* Component has a different resource `kind: Component` and `apiVersion: kustomize.config.k8s.io/v1alpha1`
<!--SR:!2025-05-31,2,240-->

## Section 12 - Kubernetes Challenges

* Kubernetes Challenges from KodeKloud site
## Section 13 - Certification Tips

* Attempt all questions. Don't get stuck on a question
* Get good with YAML
* Use short resource names

## Section 14 - Lightning Labs

* rewrite target
* cronjob concfurency
* Read the wholequestion
* set namespace
* Copy resources from docs or use k run/create

## Section 15 - Mock Exams

* Go back and validate all questions if there's enough time

## Steps to Take During Exam

* Connect webcam and set audio/video to webcam
* Disconnect headphones
* Run [Compatibility Check](https://syscheck.bridge.psiexams.com/en)
* Close all open apps except browser
* Check-in 30 minutes before
* Leave phone, watch, tab outside
* Move trash bin, amp
* Have license handy
* Run the PSI environment test 1 day before the exam
* Use `Control + Shift + C/V` in the terminal for copy/paste
* ssh into the node, set context, do the question, exit out

