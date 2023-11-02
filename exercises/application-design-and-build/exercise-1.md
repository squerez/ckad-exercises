# Exercises
In this next section, we will present exercises and solutions for each exercise.
Record your timings and try to solve without any help. 

## Exercise 1

### Problem
Create a namespace called 'mynamespace' and a pod with image nginx on the same namespace.

### Solution
<details>
  <summary>Spoiler warning</summary>
  ```
    k create ns mynamespace
    k run nginx --image=nginx --restart=Never -n mynamespace
  ```
</details>


