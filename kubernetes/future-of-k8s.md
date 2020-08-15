# Future of K8S

## Storage

`StatefulSets` is a new resource type, making Pods more persistent.
You gotta consider this if you consider working with databases.

*Brett's advice is to outsource databases to a cloud provider.*
*Cause orchestration is initially designed to provide immutable, distributed and replaceable containers.*
*Statefulness adds some complexity.*

## Volumes

Inside `spec` you can add volumes very easily, which will be tied to the lifecycle of a Pod, so all containers in a single Pod can share them.

A (new) resource called **persistent volumes** allows to directly create persistent volumes at the cluster level, and outlives a Pod. This also allows separate storage configuration from the Pod which will be using it. So, in the end, multiple pods will be able to share it.


CSI plugins are also the new way to connect to a distant storage.

## Ingress

Allows to route outside connections base on hostname or URL.
It's not installed by default. This is basically a kind of an HTTP proxy.
You could also use Traefik !


## CRD's and Operator pattern

[Here](https://coreos.com/operators/)

## Higher Deployment Abstractions

[Helm](https://helm.sh/) : helps you manage, define, install and upgrade k8s applications by using templating.

You can also use this to create yml config file which can be used for docker-compose in local development and for Kubernetes in production, thanks to ["Compose on Kubernetes"](https://kubernetes.io/fr/docs/tasks/configure-pod-container/translate-compose-kubernetes/). So you can avoid the fact to avoid a compose yaml for dev and a k8s yaml for production.

[Have at a look at this too](https://github.com/kubernetes-sigs/kustomize)

## Kubernetes dashboard

[Here.](https://github.com/kubernetes/dashboard)

Some distributions also have their own GUI (Rancher, OpenShift, etc).

## Namespaces and Context

Namespaces are essentially virtual views/cluster inside a cluster. This is not related to Linux namespaces.
Each namespace has its own context.