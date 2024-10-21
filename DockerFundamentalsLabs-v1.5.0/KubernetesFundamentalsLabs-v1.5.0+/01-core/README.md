[//]: # (Confidential document)
[//]: # (01/07/2023)
[//]: # (v 1.5.0)


# Kubernetes Fundamentals labs v1.5.0 - Core
## Namespaces

Namespaces are a logical cluster or environment. They are the primary method of partitioning a cluster or scoping access.



## Lab 1 : Namespaces 

 - Learn how to create and switch between Kubernetes Namespaces using kubectl
 
 
```
kubectl get namespaces
kubectl config get-contexts
kubectl create namespace dev
kubectl config set-context minikube --namespace=dev
kubectl config get-contexts
```

## Pods

A pod is the atomic unit of Kubernetes. It is the smallest “unit of work” or “management resource” within the system and is the foundational building block of all Kubernetes Workloads.


## Lab 2 : Pods 

 - Examine both single and multi-container Pods; including: viewing their attributes through the cli and their exposed Services through the API Server proxy.
 - Create a simple Pod called pod-example 
 - List, describe Pod
 - Logs, exec Pod
 - Use kubectl proxy to verify the web server
 
```
kubectl create -f manifests/pod-example.yaml
kubectl get po
kubectl get pod pod-example
kubectl describe pod pod-example
kubectl logs pod-example
kubectl exec -it pod-example -- sh

kubectl proxy
```
create a new ssh session and consult the URL

```
ssh -i XXX.pem -L 8001:localhost:8001 ubuntu@IP
```
-  http://127.0.0.1:8001/api/v1/namespaces/dev/pods/pod-example/proxy/

or 

```
kubectl port-forward --address 0.0.0.0 pod/pod-example 8888:80
```
-  http://publicIP:8888

```
kubectl create -f manifests/pod-multi-container-example.yaml
kubectl get po
kubectl describe po multi-container-example
kubectl logs multi-container-example
kubectl logs -c nginx multi-container-example
kubectl logs -c content multi-container-example
kubectl exec -it multi-container-example -- sh
kubectl exec -it -c nginx multi-container-example -- sh

$ kubectl proxy
```

create a new ssh session and consult the URL
```
ssh -i XXX.pem -L 8001:localhost:8001 ubuntu@IP
```
- http://127.0.0.1:8001/api/v1/namespaces/dev/pods/multi-container-example/proxy/



## Labels and Selectors

Labels are key-value pairs that are used to identify, describe and group together related sets of objects or resources.

Selectors use labels to filter or select objects, and are used throughout Kubernetes.

## Lab 3 : Labels and Selectors

 - Explore the methods of labeling objects in addition to filtering them with both equality and set-based selectors
 - labes pods
 - select pods using labels

```
kubectl label pod pod-example app=nginx environment=dev
kubectl label pod multi-container-example  app=nginx environment=prod
kubectl get pods --show-labels
kubectl get pods --selector environment=prod
kubectl get pods -l app=nginx
```


##  Services

Services within Kubernetes are the unified method of accessing the exposed workloads of Pods. They are a durable resource (unlike Pods) that is given a static cluster-unique IP and provide simple load-balancing through kube-proxy.


## Lab 4 : Services
 - Create a ClusterIP service and view the different ways it is accessible within the cluster

```
kubectl create -f manifests/service-clusterip.yaml
kubectl describe service clusterip

kubectl proxy
```
create a new ssh session and consult the URL

```
ssh -i XXX.pem -L 8001:localhost:8001 ubuntu@IP
```
-  http://127.0.0.1:8001/api/v1/namespaces/dev/services/clusterip/proxy/



## Clean up

```
kubectl delete -f manifests/

```