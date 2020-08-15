# Kubernetes management techniques


## Generators

Generators create the specifications to apply to a k8s cluster. It's kind of a template which fill be filled by your command options (image name, name, port, etc). Every k8s object have its own generator.

You can specify one using `--generator=<generator>`.

You can also output these specifications when using the CLI.

**Ouput the yaml config file equivalent of your command:**
`kubectl create deployment test --image nginx --dry-run -o yaml `

```YML
apiVersion: apps/v1
kind: Deployment
metadata:
  creationTimestamp: null
  labels:
    app: test
  name: test
spec:
  replicas: 1
  selector:
    matchLabels:
      app: test
  strategy: {}
  template:
    metadata:
      creationTimestamp: null
      labels:
        app: test
    spec:
      containers:
      - image: nginx
        name: nginx
        resources: {}
status: {}
```

`kubectl create job test --image nginx --dry-run -o yaml`
```YML
apiVersion: batch/v1
kind: Job
metadata:
  creationTimestamp: null
  name: test
spec:
  template:
    metadata:
      creationTimestamp: null
    spec:
      containers:
      - image: nginx
        name: test
        resources: {}
      restartPolicy: Never
status: {}
```

`kubectl expose deployment/test --port 80 --dry-run -o yaml`
```YML
apiVersion: v1
kind: Service
metadata:
  creationTimestamp: null
  labels:
    app: test
  name: test
spec:
  ports:
  - port: 80
    protocol: TCP
    targetPort: 80
  selector:
    app: test
status:
  loadBalancer: {}
```

## Imperative vs Declarative

There are two different ways to setup a k8s cluster.

**Imperative (focuses on how a program operates)** : using commands with `kubectl`.
**Declarative (focuses on what a program sould accomplish)** : using YAML config file(s) and `apply`.


## Three manangement approaches

Imperative commands : `run`,`expose`, `scale`, `edit`, `create deployment`
  - Best for dev/personal projects

Imperative objects : `create -f file.yml`, `replace -f file.yml`, `delete`
  - Good for prod or small env, single fil per command
  - Store your changes in git-based yaml files
  - .. but hard to automate

Declarative objects : `apply -f file.yml` or `apply -f dir\`
  - Best for prod, easy to automate
  - More conducive for infrastructure as code
  - ... but harder to understand and predict changes

**Don't mix the three approaches**
**Store the yml config files in git, and commit BEFORE you apply** *(And setup "GitOps" automation to automatically apply on your production server)*