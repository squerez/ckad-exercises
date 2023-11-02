# ckad-exercises
Tips and exercises for preparing to CKAD exam. 

## Exam details

The CKAD exam is an online proctored exam that consists of completing a set
of problems using the command line. **The exam has a duration of 2 hours to complete 15-20
questions, so at worst you only have 6 minutes per question**.

Being as fast as possible is the key to pass this exam, so as a general tip, practice a LOT
of the command line and use as much as possible abbreviations and aliases to commands.

In the next section, I will do my best to compile important exam information.  
I recommend that you read the up-to-date [official exam documentation](https://docs.linuxfoundation.org/tc-docs/certification/tips-cka-and-ckad) for completeness and correctness.


### What resources are allowed during the exam

You can use the browser within the VM to access the documentation from:

- https://kubernetes.io/docs/
- https://kubernetes.io/blog/
- https://helm.sh/docs

Subdomains and language translations of those websites are also allowed.


### Technical instructions for the exam

Adapted from the documentation:

- Root privileges can be obtained by running 'sudo −i'.
- **You must NOT reboot the base node (hostname node-1). Rebooting the base node will NOT restart your exam environment**.
- Do not stop or tamper with the certerminal process as this will END YOUR EXAM SESSION.
- Do not block incoming ports 8080/tcp, 4505/tcp and 4506/tcp. This includes firewall rules that are found within the distribution's default firewall configuration files as well as interactive firewall commands.
- Use Ctrl+Alt+W instead of Ctrl+W (this is a shortcut that closes current tab on Google Chrome).
- To copy & paste within the Linux Terminal you need to use LINUX shortcuts:
  - copy --> Ctrl+Shift+C
  - paste --> Ctrl+Shift+V
  - OR use the Right Click Context Menu and select Copy or Paste
- INSERT key is prohibited, use i for insert mode in VIM and ESC to get out of insert mode


### Exam environment

Adapted from the documentation:

- Each task on this exam must be completed on a designated cluster/configuration context.
- An infobox at the start of each task provides you with the cluster name/context information. 
- Nodes making up each cluster can be reached via ssh, using a command such as the following: ssh <nodename>
- You must return to base node (hostname node-1) after completing each task.
- Nested-ssh is not supported.
- Root privileges can be obtained on any node with 'sudo -i'
- You can also use sudo to execute commands with elevated permissions 
- You can use kubectl and the appropriate context to work on any cluster from the base node. When connected to a cluster member via ssh, you will only be able to work on that particular cluster via kubectl.
- For convenience, all environments have 'kubectl' with 'k' alias and bash autocompletion, 'jq', 'tmux', 'curl', 'wget' and 'man' tools pre-installed and configured
- Instructions for connecting to cluster nodes are provided in appropriate tasks
- If you need to destroy/recreate a resource to perform a certain task, it is your responsibility to back up the resource definition appropriately prior to destroying the resource.-
- The CKAD environment is currently running Kubernetes v1.28 and etcd v3.5

The environment will look like the following image:

![environment](https://2145393087-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M5QaeeC1mG9VndIpgJe%2Fuploads%2F13joD9D4ULTjRYNMP1eY%2FLF%20Remote%20Desktop%20070722d.png?alt=media&token=3784c329-768e-475c-b852-88ef98c899ce)


### Exam topics

The exam tests for the following domains and competencies:

- Application Design and Build (20%)
  - Define, build and modify container images
  - Understand Jobs and CronJobs
  - Understand multi-container pod design patterns (sidecar, init etc)
  - Utilize persistent and ephemeral volumes
- Application Deployment (20%)
  - Use Kubernetes primitives to implement common deployment strategies (blue/green, canary)
  - Understand Deployments and how to perform rolling updates
  - Use the Helm package manage to deploy existing packages
- Application Observability and Maintenance (15%)
  - Understand API deprecations
  - Implement probes and health checks
  - Use built-in CLI tools to monitor kubernetes applications
  - Utilize container logs
  - Debugging in Kubernetes
- Application Environment, Configuration and Security (25%)
  - Discover and use resources that extend Kubernetes (CRD, Operators)
  - Understand authentication, authorization and admission control
  - Understand request, limits, quotas
  - Understand ConfigMaps
  - Define resource requirements
  - Create and consume secrets
  - Understand ServiceAccounts
  - Understand Application Security (SecurityContexts, Capabilities)
- Services and Networking (20%)
  - Demonstrate basic understanding of NetworkPolicies
  - Provide and troubleshoot access to applications via services
  - Use Ingress rules to expose applications

## Tips

### 1. Use imperative commands
Use imperative commands to create resources instead of declarative commands. This will help you to create resources faster.

```bash
# Imperative commands
$ kubectl run nginx --image=nginx
$ kubectl expose deployment nginx --port=80 --type=NodePort
$ kubectl run nginx --image=nginx --restart=Never --dry-run -o yaml > pod.yaml
$ kubectl run nginx --image=nginx --restart=Never --dry-run -o json > pod.json
$ kubectl run nginx --image=nginx --restart=Never --dry-run -o yaml --port=80 --labels=app=nginx --requests='cpu=100m,memory=256Mi' --limits='cpu=200m,memory=512Mi' --serviceaccount=myuser --serviceaccount=myuser --serviceaccount=myuser --serviceaccount=myuser > pod.yaml
$ kubectl create ns mynamespace
$ kubectl run nginx --image=nginx --restart=Never --dry-run -o yaml --port=80 --labels=app=nginx --requests='cpu=100m,memory=256Mi' --limits='cpu=200m,memory=512Mi' --serviceaccount=myuser --serviceaccount=myuser --serviceaccount=myuser --serviceaccount=myuser --namespace=mynamespace > pod.yaml
$ kubectl run nginx --image=nginx --restart=Never --dry-run -o yaml --port=80 --labels=app=nginx --requests='cpu=100m,memory=256Mi' --limits='cpu=200m,memory=512Mi' --serviceaccount=myuser --serviceaccount=myuser --serviceaccount=myuser --serviceaccount=myuser --namespace=mynamespace --serviceaccount=myuser > pod.yaml
$ kubectl run nginx --image=nginx --restart=Never --dry-run -o yaml --port=80 --labels=app=nginx --requests='cpu=100m,memory=256Mi' --limits='cpu=200m,memory=512Mi' --serviceaccount=myuser --serviceaccount=myuser --serviceaccount=myuser --serviceaccount=myuser --namespace=mynamespace --serviceaccount=myuser --serviceaccount=myuser > pod.yaml
$ kubectl run nginx --image=nginx --restart=Never --dry-run -o yaml --port=80 --labels=app=nginx --requests='cpu
────────────────────────────────────────────────────────────────────────

## General tips

* [Kubernetes the hard way](
────────────────────────────────────────────────────────────────────────
## Cluster Architecture, Installation & Configuration (25%)
### 1. Understand the Kubernetes API primitives.
#### 1.1. Create and Configure Basic Pods
* Create a pod named `nginx-pod` with image `nginx` and expose it on container port 80
* Create a pod named `redis-pod` with image `redis:alpine` and expose it on container port 6379
* Create a pod named `mysql-pod` with image `mysql:5.6` and expose it on container port 3306
* Create a pod named `httpd-pod` with image `httpd:alpine` and expose it on container port 80
* Create a pod named `centos-tools` with image `centos/tools`. Sleep for 10000 seconds
* Create a pod named `busybox` with image `busybox` and command `sleep 1000`
* Create a pod named `secret-pod` with image `redis:alpine` that runs a container with env variable `REDIS_PASSWORD=redis123`
* Create a pod named `two-containers` with image `nginx`, and container `nginx` listening on port 80 and `busybox` sleeping for 10000 seconds
* Create a pod named `webapp-color` with image `kodekloud/webapp-color` and env variable APP_COLOR=blue
* Create a pod named `webapp-color` with image `kodekloud/webapp-color` and env variable APP_COLOR=green
* Create a pod named `multi-pod` with image `nginx`, `redis:alpine` and `busybox` sleeping for 10000 seconds
* Create a pod named `multi-pod` with image `nginx`, `redis:alpine` and `busybox` sleeping for 10000 seconds. Configure redis pod with a env variable `DB_Host=postgres`
* Create a pod named `counter` with image `redis:alpine` and env variable `COUNTER=1` and command redis-server. Configure the pod so that the env variable is set to `COUNTER=2` and the command is set to redis-server `/redis-master/redis.conf`
* Create a pod named `counter` with image `redis:alpine` and env variable `COUNTER=1` and command redis-server. Configure the pod so that the env variable is set to `
────────────────────────────────────────────────────────────────────────

## Tips
- Use `kubectl explain` to get a description of a resource.
- Use `kubectl explain <resource>.<field>` to get a description of a specific field.
- Use `kubectl run` to create a deployment.
- Use `kubectl create` to create resources from a file.
- Use `--dry-run` and `-o yaml` to create a resource template.
- Use `kubectl edit` to edit a resource in an editor.
- Use `kubectl explain pod.spec.containers` to see what fields are available for a container.
- Use `kubectl set image` to update the image of a container in a deployment.
- Use `kubectl rollout` to manage rollouts.
- Use `kubectl create secret` to create secrets.
- Use `kubectl create configmap` to create configmaps.
- Use `kubectl auth can-i` to check permissions.
- Use `kubectl auth can-i --list` to list all permissions.
- Use `kubectl api-resources` to list all resources.
- Use `kubectl api-versions` to list all versions of all resources.
- Use `kubectl api-resources --namespaced=false` to list all non-namespaced resources.
- Use `kubectl api-resources --verbs=list --namespaced=false` to list all resources that support the list verb.
- Use `kubectl api-resources --api-group=extensions` to list all resources in the extensions group.
- Use `kubectl api-resources -o name` to list all resources in a compact format.
- Use `kubectl api-resources --sort-by=name` to list all resources sorted by name.
- Use `kubectl explain pods.spec --recursive` to get a description of a resource and all of its children.
- Use `kubectl explain pods.spec --recursive | grep -e "name:" -e "REQUIRED"` to get a description of a resource and all of its required children.
- Use `kubectl explain pods.spec --recursive | grep -e "name:" -e "optional"` to get a description of a resource and all of its optional children.
- Use `kubectl explain pods.spec --recursive | grep -e "name:" -e "default"` to get a description of a resource and all of its children that have a default value.
- Use `kubectl explain pods.spec --recursive | grep -e "name:" -e "default" -e "REQUIRED"` to get a description of a resource and all of its required children that have a default value
────────────────────────────────────────────────────────────────────────

## Tips

- [CKAD Tips](./tips/ckad-tips.md)

## Exercises

- [Core Concepts - 13%](./exercises/core-concepts.md)
- [Multi-Container Pods - 10%](./exercises/multi-container-pods.md)
- [Pod Design - 20%](./exercises/pod-design.md)
- [State Persistence - 8%](./exercises/state-persistence.md)
- [Configuration - 18%](./exercises/configuration.md)
- [Observability - 18%](./exercises/observability.md)
- [Services and Networking - 13%](./exercises/services-and-networking.md)

## Useful Links

- [Kubernetes Documentation](https://kubernetes.io/docs/home/)
- [Kubernetes Reference](https://kubernetes.io/docs/reference/)
- [Kubernetes Learning Resources](https://kubernetes.io/docs/home/#kubernetes-learning-resources)
- [Kubernetes By Example](http://kubernetesbyexample.com/)
- [Kubernetes the hard way](
────────────────────────────────────────────────────────────────────────

## Tips

* [CKAD Exam Tips](
────────────────────────────────────────────────────────────────────────

# Pre-requisites
- [ ] [Kubernetes the hard way](
────────────────────────────────────────────────────────────────────────

## Tips

- [Tips](#tips)
  - [1. Practice, practice, practice](#1-practice-practice-practice)
  - [2. Learn how to use the [Kubernetes Documentation](https://kubernetes.io/docs/home/)](#2-learn-how-to-use-the-kubernetes-documentationhttpskubernetesiodocshome)
  - [3. Learn how to use [kubectl explain](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#explain)](#3-learn-how-to-use-kubectl-explainhttpskubernetesiodocsreferencegeneratedkubectlkubectl-commandsexplain)
  - [4. Learn how to use [kubectl cheat sheet](https://kubernetes.io/docs/reference/kubectl/cheatsheet/)](#4-learn-how-to-use-kubectl-cheat-sheethttpskubernetesiodocsreferencekubectlcheatsheet)
  - [5. Learn how to use [kubectl imperative commands](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#apply)](#5-learn-how-to-use-kubectl-imperative-commandshttpskubernetesiodocsreferencegeneratedkubectlkubectl-commandsapply)
  - [6. Learn how to use [kubectl explain](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#explain)](#6-learn-how-to-use-kubectl-explainhttpskubernetesiodocsreferencegeneratedkubectlkubectl-commandsexplain)
  - [7. Learn how to use [kubectl explain](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#explain)](#7-learn-how-to-use-kubectl-explainhttpskubernetesiodocsreferencegeneratedkubectlkubectl-commandsexplain)
  - [8. Learn how to use [kubectl explain](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#explain)](#8-learn-how-to-use-kubectl-explainhttpskubernetesiodocsreferencegeneratedkubectlkubectl-commandsexplain)
  - [9. Learn how to use [kubectl explain](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#explain)](#9-learn-how-to-use-kubectl-explainhttpskubernetesiodocsreferencegeneratedkubectlkubectl-commandsexplain)
  - [10. Learn how to use [kubectl explain](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#explain)](#10-learn-how-to-use-kubectl-explainhttpskubernetesiod
────────────────────────────────────────────────────────────────────────

## 1. Core Concepts - 13%
### 1.1. Understand Kubernetes API primitives
#### 1.1.1. Create and configure basic Pods
- Pod yaml file
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: pod-1
spec:
  containers:
  - name: container-1
    image: nginx
    ports:
    - containerPort: 80
```
- Create pod
```bash
kubectl create -f pod.yaml
```
- Get pod
```bash
kubectl get pods
```
- Get pod details
```bash
kubectl describe pod pod-1
```
- Delete pod
```bash
kubectl delete pod pod-1
```
#### 1.1.2. Understand how to create and configure basic ReplicationSets
- ReplicationSet yaml file
```yaml
apiVersion: apps/v1
kind: ReplicationSet
metadata:
  name: rs-1
spec:
  replicas: 3
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      name: nginx
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx
        ports:
        - containerPort: 80
```
- Create ReplicationSet
```bash
kubectl create -f rs.yaml
```
- Get ReplicationSet
```bash
kubectl get rs
```
- Get ReplicationSet details
```bash
kubectl describe rs rs-1
```
- Delete ReplicationSet
```bash
kubectl delete rs rs-1
```
#### 1.1.3. Pod lifecycle
- Pod yaml file
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: pod-1
spec:
  containers:
  - name: container-1
    image: nginx
    ports:
    - containerPort: 80
```
- Create pod
```bash
kubectl create -f pod.yaml
```
- Get pod
```bash
kubectl get pods
```
- Get pod details
```bash
kubectl describe pod pod-1
```
- Delete pod
```bash
kubectl delete pod pod-1
```
#### 1.1.4. Understand ConfigMaps
- ConfigMap yaml file
```yaml
apiVersion
────────────────────────────────────────────────────────────────────────

## Exercises

### Core Concepts - 13%
- [x] [Create a Namespace](exercises/core-concepts/create-namespace.md)
- [x] [Create a Pod](exercises/core-concepts/create-pod.md)
- [x] [Get a Pod's Log](exercises/core-concepts/get-pod-log.md)
- [x] [List Pods](exercises/core-concepts/list-pods.md)
- [x] [Describe a Pod](exercises/core-concepts/describe-pods.md)
- [x] [Delete a Pod](exercises/core-concepts/delete-pod.md)
- [x] [Create a Deployment](exercises/core-concepts/create-deployment.md)
- [x] [Get Deployment Status](exercises/core-concepts/get-deployment-status.md)
- [x] [Describe a Deployment](exercises/core-concepts/describe-deployment.md)
- [x] [Update a Deployment](exercises/core-concepts/update-deployment.md)
- [x] [Rollback a Deployment](exercises/core-concepts/rollback-deployment.md)
- [x] [Scale a Deployment](exercises/core-concepts/scale-deployment.md)
- [x] [Pause a Deployment](exercises/core-concepts/pause-deployment.md)
- [x] [Resume a Deployment](exercises/core-concepts/resume-deployment.md)
- [x] [Delete a Deployment](exercises/core-concepts/delete-deployment.md)
- [x] [Create a Service](exercises/core-concepts/create-service.md)
- [x] [List Services](exercises/core-concepts/list-services.md)
- [x] [Describe a Service](exercises/core-concepts/describe-service.md)
- [x] [Delete a Service](exercises/core-concepts/delete-service.md)
- [x] [Create a Job](exercises/core-concepts/create-job.md)
- [x] [List Jobs](exercises/core-concepts/list-jobs.md)
- [x] [Describe a Job](exercises/core-concepts/describe-job.md)
- [x] [Delete a Job](exercises/core-concepts/delete-job.md)
- [x] [Create a CronJob](exercises/core-concepts/create-cronjob.md)
- [x] [List CronJobs](exercises/core-concepts/list-cronjobs.md)
- [x]
