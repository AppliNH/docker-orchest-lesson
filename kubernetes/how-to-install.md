# How to install

If you have **Docker Desktop**, then you just have to enable K8S from the settings pan (it also manages the install of **kubectl**, and uses a small Linux VM for your clusters).

If you have **Docker Toolbox**, use **miniKube** which is kind of a small Linux VM (you'll have also to install **kubectl**).

If you're on a **Linux** host, use **microK8s** (then control the service via the `microk8s` command) (also gives you access to **kubectl** via the `microk8s.kubectl`command, so think about setting up an alias).

If you wanna try k8s in the **browser**, you can go to https://play-with-k8s.com or https://www.katacoda.com/courses/kubernetes/playground.

## Ressources

- [Minikube installer](https://github.com/kubernetes/minikube/releases/)
    - Minikube runs in VirtualBox (by default) and has its own IP. Find that with `minikube ip`.
- [Kubectl install instructions](https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-kubectl-on-windows)
- [MicroK8S install instructions](https://github.com/ubuntu/microk8s)
    - `sudo snap install microk8s --classic --channel=1.17/stable`
    - `microk8s.enable dns`
    - `microk8s.status`
    - ... and you should be good to go :)



