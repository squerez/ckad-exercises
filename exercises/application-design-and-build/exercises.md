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

