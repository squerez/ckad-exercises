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

