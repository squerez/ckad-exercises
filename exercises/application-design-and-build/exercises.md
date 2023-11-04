# Exercises
In this next section, we will present exercises and solutions for each exercise.
Record your timings and try to solve without any help. 

## Exercise 1

### Problem
Create a namespace called 'gin' and a pod with image nginx on the same namespace.

### Solution
<details>
  <summary>Spoiler warning</summary>

  ```
    k create ns gin
    k run nginx --image=nginx --restart=Never -n gin
  ```

</details>


## Exercise 2

### Problem
Create a pod with the name 'nginx' and image 'nginx' and expose it on port 80 on the same namespace.
After this, delete the pod and use a different imperative command to do the same operation.

### Hint

<details>
  <summary>Spoiler warning</summary>

  Imperative commands that create objects are 'create' and 'run'.

</details>

### Solution
<details>
  <summary>Spoiler warning</summary>

  ```
    k run nginx --image=nginx --restart=Never -n gin --port=80
    k delete pod nginx -n gin
    k create deploy nginx --name=nginx --port=80 -n gin
  ```

</details>


## Exercise 3

### Problem
Create a dry-run pod with the name 'nginx' and image 'nginx' and expose it on port 80 on the same namespace. 
Save the resulting manifest as YAML.

### Solution
<details>
  <summary>Spoiler warning</summary>

  ```
    k create deploy nginx --image=nginx -n gin --port=80 --dry-run=client -o yaml > pod.yaml
    k create -f pod.yaml
    or 
    k run nginx --image=nginx --restart=Never --port=80 --dry-run=client -o yaml > k create -n gin -f -
  ```

</details>


## Exercise 4

### Problem
Create a busybox pod using a YAML manifest that runs "env" as a command. 
Check the logs created and use the default namespace.

### Solution
<details>
  <summary>Spoiler warning</summary>

  ```
    k run busybox --image=busybox --restart=Never --dry-run=client -o yaml --command -- env > busybox.yaml
    cat busybox.yaml
    k apply -f busybox.yaml
    k logs pod busybox 
  ```

</details>


## Exercise 5

### Problem
Generate a YAML definition for a namespace named 'nogin' without creating a new namespace.

### Solution
<details>
  <summary>Spoiler warning</summary>

  ```
    k create ns nogin --dry-run=client -o yaml 
  ```

</details>


## Exercise 6

### Problem
Create a Pod Resource Quota for the gin namespace, with a hard limit of 2 pods, 1 Gb of memory and 1 cpu.
The quota should be named "pod-quota" and save as a YAML to apply later.

### Solution
<details>
  <summary>Spoiler warning</summary>

  ```
    k create quota pod-quota --hard=pods=2,cpu=1,memory=1Gi --dry-run=client -o yaml > pod-quota.yaml
    k apply -f pod-quota.yaml
  ```

</details>


## Exercise 7

### Problem
Set a Resource Quota for the total memory and CPU to be used on all pods running in the 'nogin' namespace.
The quotas are as follows:

-  The memory request total for all Pods in that namespace must not exceed 1 GiB.
-  The memory limit total for all Pods in that namespace must not exceed 2 GiB.
-  The CPU request total for all Pods in that namespace must not exceed 1 cpu.
-  The CPU limit total for all Pods in that namespace must not exceed 2 cpu.

### Solution
<details>
  <summary>Spoiler warning</summary>

  ```
    k create quota all-pod-quota -n nogin --hard=requests.cpu=1,requests.memory=1Gi,limits.cpu=2,limits.memory=2Gi --dry-run=client -o yaml > all-pod-quota.yaml
    k apply -f all-pod-quota.yaml
  ```

</details>


## Exercise 8

### Problem
After creating the quota above, query the used values and pretty-print the output.

### Solution
<details>
  <summary>Spoiler warning</summary>

  ```
    k get quota all-pod-quota -n nogin -o jsonpath='{ .status.used }' | jq .
  ```

</details>


## Exercise 9

### Problem
Create a stress pod with memory request and limits applied to a container in the 'gin' namespace.
Here are the limit/requests definition:

- The container should have a memory request of 100 MiB
- The container should have a memory limit of 200 MiB

In addition, it should run the 'stress' command in the following arguments:

- --vm = 1
- --vm-bytes = 150M
- --vm-hang = 1

Use the "polinux/stress" image in the container.

### Solution
<details>
  <summary>Spoiler warning</summary>

  ```
    k run memory-limits -n gin --image=polinux/stress --dry-run=client -o yaml --command -- stress > memory-limits.yaml

    # Edit the memory-limits.yaml and add the args, resource requests and limits. It should look like this:

	apiVersion: v1
	kind: Pod
	metadata:
	  labels:
		run: memory-demo
	  name: memory-demo
      namespace: gin
	spec:
	  containers:
	  - name: memory-demo
		image: polinux/stress
		resources:
		  requests: 
			memory: "100Mi"
		  limits:
			memory: "200Mi"
		command: ["stress"]
		args: ["--vm", "1", "--vm-bytes", "150M", "--vm-hang", "1"]
	status: {}

	# Save the file and run the next command
    k apply -f memory-limits.yaml
  ```

</details>

## Exercise 10

### Problem
Create a Pod


### Solution
<details>
  <summary>Spoiler warning</summary>

  ```
  ```

</details>
