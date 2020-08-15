# Expose containers with service

A service is a stable address for pod(s).
CoreDNS allows to resolve services by name.

There are different service types/abstractions :

#### Cluster IP

Only available in the cluster, this is the default type. It's only reachable from within the cluster (nodes and pods), which means it can be accessed by the other pods of this same service. It basically allows pods to talk to each others.


#### NodePort

Designed for something outside the cluster to dialog with the cluster. It's an high port, which will allow anyone to reach the node.

#### LoadBalancer

Controls LoadBalance endpoint which external to the cluster. This is available when your infrastructure (can be cloudProvider such as AWS/Azure/GCP) is providing a LoadBalancer. This is for traffic coming inside of the cluster from external source with load balancing purposes.

#### ExternalName

Adds CNAME DNS record to CoreDNS. Not used for pods, but for giving pods a DNS name to use for something outside Kubernetes (for remote work for example).

#### Ingress

Specifically designed for HTTP traffic, have a look [here]().


## Create a ClusterIP Service

Steps:
**Create a deployment:**
`kubectl create deployment httpenv --image=bretfisher/httpenv`

**Scale pod's replicas:**
`kubectl scale deployment/httpenv --replicas=5`

**Expose the deployment:**
`kubectl expose deployment/httpenv --port 8888`

****

This creates a clusterIP service, which is reachable inside of the cluster on port 8888.
You can see the created service using `kubectl get service`.

If you're on Windows/MacOS you can curl the service, using first this :

`kubectl run --generator run-pod/v1 tmp-shell --rm -it --image bretfisher/netshoot -- bash`
and then:

`curl httpenv:8888`

This is because a clusterIP service is not available outside the cluster :)
So here, you basically run another pod to get in.

However, this is more precisely because Windows/MacOS are not on the same cluster as the one we just created, and that we're running our cluster in a small Linux VM.
On Linux, you can `curl <serviceIpAdress>:8888` and it will work.



## Create a NodePort service

**Expose the port 8888 as a NodePort service, so it can be accessed externally:**
`kubectl expose deployment/httpenv --port 8888 --name httpenv-np --type NodePort`
*Note: a NodePort service creates a ClusterIP service too*
*Note2: LoadBalancer services creates a NodePort and ClusterIP services too*


Now, have a look at `kubectl get services` and see on which port of your host the NodePort is forwarded.
You can `curl localhost:<thatPort>` to get an answer.

## Create a LoadBalancing service

`kubectl expose deployment/httpenv --port 8888 --name httpenv-lb --type LoadBalancer`
*Note: if you're on kubeadm, minikube or microk8s there's no built-in LoadBalancer, so the command will stay as "pending".*




