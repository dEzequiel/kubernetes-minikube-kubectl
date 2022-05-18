
# **Table of content**
- [**Table of content**](#table-of-content)
- [Introduction](#introduction)
  - [Problems](#problems)
  - [Orchestration with Kubernetes](#orchestration-with-kubernetes)
  - [What Kubernetes provide to us](#what-kubernetes-provide-to-us)
- [Minikube](#minikube)
  - [Install Minikube](#install-minikube)
- [Kubectl](#kubectl)
  - [Install Kubectl](#install-kubectl)

# Introduction

In this README we are going to explore the problems **Kubernetes** solve and what it provides us. In addition to the installation process of **Minikube** and **Kubectl**.

## Problems

Having an application that works as a stack with different layers located within a single machine leads to a problem that is dependency control.

To solve the above, a new form of organization was migrated, which is to isolate each application in a virtual machine under a local machine. The problem of dependencies is solved, since they are isolated between them. But a new problem appears and it is the consumption received by the machine where the other virtual machines reside.

The solution to the two problems mentioned above is what is known as a container. Each contain runs as a separate process from the others within the same operating system.

This new way solves problems, but it also comes with a set of problems of its own.

How do you ensure that containers run and heal when they are unhealthy?

What would happen if you suddenly see a spike and want to scale up your containers automatically?

 What if you see a downward surge in traffic and want to scale down your containers to the optimal level?

How would you make sure that the containers can talk to each other?

**The answer to all these questions is a container orchestration platform like Kubernetes.**

## Orchestration with Kubernetes

The idea of using Kubernetes is simple. You have a cluster of servers that are managed by Kubernetes, and Kubernetes is responsible for orchestrating your containers within the servers. You treat servers as servers, and you run applications within self-contained units called containers.

Since containers can run the same in any server, it does not matter on what server your container is running, as long as the client can reach it.

Kubernetes uses a simple concept to manage containers. There are master nodes (control plane) which control and orchestrate the container workloads, and the worker nodes where the containers run. Kubernetes run containers in pods, which form the basic building block in Kubernetes.

## What Kubernetes provide to us

1. **Communication with the container runtime** *kubelet* component runs as a service on each node and is responsible for communicating with the container platform to manage that container.

1. **Store configuration state** using *kubectl.*

1. **Provides a software-based abstract network orchestration layer** Kubernetes ensures that
containers can communicate with each other in some kind of network
overlay or bridge This network is administered within the time of
running the container (using Docker bridge networks, for
example) or through an internal or external network. When a pod
communicates with another pod, Kubernetes modifies the routing tables
to ensure connectivity is in place.

1. **Provides built-in service discovery** Kubernetes provides container service discovery out of the box. You do not need an external application to manage it. Services can also expose their pods to internal and external clients by creating listeners within their nodes.

1. **Verify the configuration** Kubernetes ensures that the
container workloads running inside the cluster
have the expected state, and if not, destroy and re-create the containers.

1. **Request objects from cloud provider** If you are running Kubernetes within a cloud provider, you can use cloud APIs to dynamically provision resources such as storage and load balancers.

# Minikube

It is a tool that manages virtual machines running on a Kubernetes instance on a single node.

## Install Minikube

We can find the file adapted to our machine on the [official page](https://minikube.sigs.k8s.io/docs/start/).

Download the binary

```curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
sudo install minikube-linux-amd64 /usr/local/bin/minikube
```


We start our *cluster* with the following command and if everything has gone well, the installation progress will be seen on the screen.

```jsx
minikube start
```

```
😄  minikube v1.25.2 en Ubuntu 20.04
✨  Controlador docker seleccionado automáticamente. Otras opciones: virtualbox, none, ssh
👍  Starting control plane node minikube in cluster minikube
🚜  Pulling base image ...
💾  Descargando Kubernetes v1.23.3 ...
    > gcr.io/k8s-minikube/kicbase: 379.06 MiB / 379.06 MiB  100.00% 517.00 KiB
    > preloaded-images-k8s-v17-v1...: 505.68 MiB / 505.68 MiB  100.00% 596.15 K
🔥  Creando docker container (CPUs=2, Memory=2200MB) ...
🐳  Preparando Kubernetes v1.23.3 en Docker 20.10.12...
    ▪ kubelet.housekeeping-interval=5m
    ▪ Generando certificados y llaves
    ▪ Iniciando plano de control
    ▪ Configurando reglas RBAC...
🔎  Verifying Kubernetes components...
    ▪ Using image gcr.io/k8s-minikube/storage-provisioner:v5
🌟  Complementos habilitados: storage-provisioner, default-storageclass
💡  kubectl not found. If you need it, try: 'minikube kubectl -- get pods -A'
🏄  Done! kubectl is now configured to use "minikube" cluster and "default" namespace by default
```


If **minikube** was installed correctly we can search for version.
```jsx
minikube version --short

v1.25.2
```

# Kubectl

The Kubernetes command-line tool, [kubectl](https://kubernetes.io/docs/reference/kubectl/kubectl/) allows you to run commands against Kubernetes clusters. You can use kubectl to deploy applications, inspect and manage cluster resources,
and view logs.

## Install Kubectl

We can find the file adapted to our machine on the [official page](https://kubernetes.io/docs/tasks/tools/)

Download latest version of *kubectl*.
```jsx
curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
```

Optionally we can validate the binary to be able to continue without fear.
```jsx
curl -LO "https://dl.k8s.io/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl.sha256"
echo "$(cat kubectl.sha256)  kubectl" | sha256sum --check
```

If it is valid the output will be
```jsx
	kubectl: La suma coincide
```

Install **kubectl**
```jsx
sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl
```

And to verify that everything has been correct we can look for the installed version.
```jsx
kubectl version --client
Kustomize Version: v4.5.4
```
