# Pods creation

*Keep in mind that there are lot of ways to do things.*

[Kubectl cheatsheet](https://kubernetes.io/docs/reference/kubectl/cheatsheet/)

Three ways to create pods from the kubectl CLI :

- `kubectl run`
- `kubectl create` (from CLI or YML config file)
- `kubectl apply` (create/update via YML config file)

## Creating pods and managing them

Two ways : via commands or YML.

**Run a pod of the nginx web sever :**
`kubectl run my-nginx --image nginx` 
or
`kubectl create deployment mynginx --image=nginx`

Before 1.18, this command creates a Deployment named `nginx`, which creates a ReplicaSet, which creates a Pod (have a look at [here](./architect-terminology)). 

**Get the list of pods:**
`kubectl get pods`
*(`-w` allows to watch)*

**Get the list of all entities (service, controller, pod):**
`kubectl get all`

**Delete a deployment:**
`kubectl delete deployment my-nginx`

**Delete anything:**
`kubectl delete <service/pod>/<name>`
*(ex `kubectl delete pod/my-pod`)*

## Future of `kubectl run`

Note down that the current goal regarding this command is to reduce its features to only create pods, so it won't create a Deployment controller anymore.
It's only fine for running one-shot containers, for troubleshooting or else.
Use `kubectl create` instead.