# Setting up cluster with declarative K8S yml files

One command : `kubectl apply -f file.yml`

You can also point to a directory full of yml files : `kubectl apply -f ymlfiles/`

You can even point to an url : `kubectl apply -f https://me.me/file.yml`

## Kubernetes YML config files

A k8s yml file needs at least four parts (four keys):

- `apiVersion`: have a look at `kubectl api-versions`
- `kind`: Pod/Deployment/Service.. `kubectl api-resources`
- `metadata`: only `name` is required in there.
- `spec` : where all the core config is, and it's gonna be totally different regarding the kind of configuration you're writing.

## Examples files

In the `kubernetes/ymlFilesExamples` directory

## Building your own YML config file

Start with the `kind` key, and have a look at all the **API** and **Kinds** available using `kubectl api-resources`.
Then `apiVersion`, have a look at all the available api versions with `kubectl api-versions`.

Right after `metadata` you'll have to have a look at `spec`.

You can browse all the different keys for a specific kind by using `kubectl explain <kind> --recursive`.
If you need more details, you can use `kubectl explain <kind>.spec` or more specifically `kubectl explain <kind>.spec.<key>` which might be easier to read if you're looking for documentation on a specific key. This also works with sub-keys *(key.sub_key.sub-sub)*.

You can also browse the API doc [on the official website](https://kubernetes.io/docs/reference/#api-reference)

## Labels and Selectors

### Labels

**Labels** go under `metadata` in the YAML.
It's a simple list of **custom key-values** for identifying your object later by selecting, gouping, or filtering for it.

It gives you the possibility to manage your objects like this:
`kubectl get pods -l app=nginx`
*This will look for a pod which has a label named "app" and for value "nginx".*

You can also use it with `apply`, to apply only resouces with a certain label:
`kubectl apply -f file.yml -l app=nginx`

### Label Selectors

You can also use labels with `selector` in the config file so your objects can find each other if they need to be linked in the cluster *(ex: a controller and a service, have a look at kubernetes/ymlFilesExamples/ex3.yml )*.

##### Basic example

Here with the custom label `app: app-nginx`.

```YML
apiVersion: v1
kind: Service
metadata:
    name: app-nginx-service
spec:
  type: NodePort
  [...]
  selector: 
    app: app-nginx
---
apiVersion: apps/v1
kind: Deployment
metadata:
  name: app-nginx-deployment
spec:
  [...]
  selector: 
    matchLabels:
      app: app-nginx # Don't forget to declare the custom label as a matchLabel too !!!
  template:
    metadata:
      labels:
        app: app-nginx 
    [...]
```

## Commands

When you're done, start your cluster using `kubectl apply -f file.yml`.


You can update it using the same command. However, if you wanna know if there are actual config changes between the running cluster and your yaml file, you can use `kubectl apply -f file.yml --server-dry-run` which will tell you where changes will occur on the running cluster.

The command `kubectl diff -f file.yml` will show more precisely the differences in details, on the file.




