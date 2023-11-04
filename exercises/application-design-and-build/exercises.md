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

-  requests cpu = 1 
-  requests memory = 1Gi 
-  limits cpu = 2
-  limits memory = 2Gi 


### Solution
<details>
  <summary>Spoiler warning</summary>

  ```
    k create quota all-pod-quota -n nogin --hard=requests.cpu=1,requests.memory=1Gi,limits.cpu=2,limits.memory=2Gi --dry-run=client -o yaml > all-pod-quota.yaml
    k apply -f all-pod-quota.yaml

  ```

</details>
