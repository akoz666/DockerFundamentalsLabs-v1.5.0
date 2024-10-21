[//]: # (Confidential document)
[//]: # (01/07/2023)
[//]: # (v 1.5.0)

# Kubernetes Fundamentals labs v1.5.0
## Training Program

1. Introduction to Kubernetes
- Project Overview
- Key Concepts
2. Architecture Overview
- Control Plane
- Node
3. Kubernetes Networking
- Container Network Interface (CNI)
- CNI Plugins
4. Concepts and Resources
- Core Objects
  - Namespaces
  - Pods
  - Labels
  - Selectors
  - Services
  - Instructor demo
  - Labs (3)
- Workloads
  - ReplicaSet
  - Deployment
  - DaemonSet
  - StatefulSet
  - Job
  - CronJob
  - Instructor demo
  - Labs (5)
- Stockage
  - Volumes
  - Persistent Volumes
  - Persistent Volume Claims
  - Dynamic/static provisioning
  - Storage Classes
  - Instructor demo
  - Labs (1)
- Configuration
  - ConfigMaps
  - Secrets
  - Instructor demo
  - Labs (2)
5. Mini Project (Sample application)
- Architecture review
- Database 
- Application Server

## Labs

minikube is local Kubernetes, focusing on making it easy to learn and develop for Kubernetes.

All you need is Docker (or similarly compatible) container or a Virtual Machine environment, and Kubernetes is a single command away: minikube start

*What you’ll need*

- 2 CPUs or more
- 2GB of free memory
- 20GB of free disk space
- Internet connection
- Container or virtual machine manager, such as: Docker, Hyper-V, VirtualBox ...

For more details :[Minikube Site](https://minikube.sigs.k8s.io/docs/start/).

Are you ready. Now, go Labs :)

```
minikube start --driver=docker  --cni=cilium
kubectl get po -A
kubectl get namespaces
kubectl config get-contexts
```

To download the labs you can use the following command
```
scp -i key.pem -r ubuntu@myip:/home/ubuntu/KubernetesFundamentalsLabs-v1.5.0+/ "$(pwd)"
```
