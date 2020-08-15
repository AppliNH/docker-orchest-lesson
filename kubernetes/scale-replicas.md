# Scale replicas

**Run a pod + deploy + replicaset:**
`kubectl run my-apache --image httpd`

**Scale the pod's replica to 2:**
`kubectl scale deploy/my-apache --replicas 2`
or 
`kubectl scale deployment my-apache --replicas 2`
*(deply = deployment = deployments)*


**This command does the following :**
- Deployment updated to 2 replicas
- ReplicaSet Controller sets pod count to 2
- Control Plane assigns node to pod
- Kubelet sees pod is needed, and starts the container

