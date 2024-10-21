[//]: # (Confidential document)
[//]: # (01/07/2023)
[//]: # (v 1.5.0)


# Kubernetes Fundamentals labs v1.5.0 - Workloads

Workloads within Kubernetes are higher level objects that manage Pods or other higher level objects.

## ReplicaSets

ReplicaSets are the primary method of managing Pod replicas and their lifecycle. This includes their scheduling, scaling, and deletion.

Their job is simple, always ensure the desired number of replicas that match the selector are running.

## Lab 1 : ReplicaSets 

 - Create and scale a ReplicaSet. Explore and gain an understanding of how the Pods are generated from the Pod template, and how they are targeted with selectors.
 - create a ReplicaSet called rs-example with 3 replicas
 - Scale ReplicaSet rs-example up to 5 replicas
 - Create an independent Pod manually with the same labels (the Pod is created and immediately terminated)
 - Delete the ReplicaSet
 
```
kubectl create -f manifests/rs-example.yaml
kubectl get pods --watch --show-labels
kubectl describe rs rs-example
kubectl scale replicaset rs-example --replicas=5
kubectl describe rs rs-example
kubectl scale rs rs-example --replicas=3
kubectl get pods --show-labels --watch
kubectl create -f manifests/pod-rs-example.yaml
kubectl get pods --show-labels --watch
kubectl describe rs rs-example
kubectl delete rs rs-example
```
##  Deployments

Deployments are a declarative method of managing Pods via ReplicaSets. They provide rollback functionality in addition to more granular update control mechanisms.

## Lab 2 : Deployments

 - Create, update and scale a Deployment as well as explore the relationship of Deployment, ReplicaSet and Pod.
 - Create a Deployment deploy-example
 - Check the status of the Deployment
 - Describe the generated ReplicaSet
 - Update the deploy-example manifest and add a few additional labels to the Pod template
 - Apply the change with the --record flag
 - View the history of a Deployment
 - View the specific revision with the summary of the Pod Template
 - Rollback to older revision
 - Delete the Deployment


```
kubectl create -f manifests/deploy-example.yaml --record
kubectl get deployments
kubectl get rs --show-labels
kubectl describe rs deploy-example-<pod-template-hash>
kubectl get pods --show-labels
kubectl describe pod deploy-example-<pod-template-hash-<random>
```
update the deploy-example.yaml (add version:1.0.0 in the pod template labels)
  template:
    metadata:
      labels:
        app: nginx
        version: 1.0.0

```
kubectl apply -f manifests/deploy-example-update.yaml --record
kubectl get pods --show-labels --watch
kubectl get rs --show-labels
kubectl scale deploy deploy-example --replicas=5
kubectl get rs --show-labels
kubectl describe deploy deploy-example
kubectl describe rs deploy-example-<pod-template-hash>
kubectl describe pod deploy-example-<pod-template-hash-<random>

kubectl rollout history deployment deploy-example
kubectl rollout history deployment deploy-example --revision=1
kubectl rollout history deployment deploy-example --revision=2
kubectl rollout undo deployment deploy-example --to-revision=1
kubectl get pods --show-labels --watch
kubectl describe deployment deploy-example
kubectl delete deploy deploy-example
```

##  DaemonSets

DaemonSets ensure that all nodes matching certain criteria will run an instance of the supplied Pod.

They bypass default scheduling mechanisms and restrictions, and are ideal for cluster wide services such as log forwarding, or health monitoring.

## Lab 3 : DaemonSets
 - Experience creating, updating, and rolling back a DaemonSet. Additionally delve into the process of how they are scheduled and how an update occurs
 - Create DaemonSet ds-example
 - Describe the Ds
 - Label the node with nodeType=edge
 - View the current Pods and display their labels with --show-labels


```
kubectl create -f manifests/ds-example.yaml --record
kubectl get daemonset
kubectl label node minikube nodeType=edge
kubectl get daemonsets
kubectl get pods --show-labels
kubectl delete ds ds-example
```

##  StatefulSets
The StatefulSet controller is tailored to managing Pods that must persist or maintain state. Pod identity including hostname, network, and storage can be considered persistent.

They ensure persistence by making use of three things:

- The StatefulSet controller enforcing predicable naming, and ordered provisioning/updating/deletion.
- A headless service to provide a unique network identity.
- A volume template to ensure stable per-instance storage.


## Lab 4 : StatefulSets
- Create, update, and delete a StatefulSet to gain an understanding of how the StatefulSet lifecycle differs from other workloads with regards to updating, deleting and the provisioning of storage
- Create StatefulSet sts-example 
- View pods
- View the current Persistent Volume Claims
- Delete the sts-example-2 Pod
- Check pods
- Scale and check Persistent Volume Claims
- Delete sts

```
kubectl create -f manifests/sts-example.yaml
kubectl get pods --show-labels --watch
kubectl describe statefulset sts-example
kubectl get pvc
kubectl delete pod sts-example-2
kubectl get pods 

kubectl scale sts sts-example --replicas=5
kubectl get pods 
kubectl get pvc
kubectl scale sts sts-example --replicas=3
kubectl get pods 
kubectl get pvc
kubectl delete sts sts-example
kubectl delete pvc --all
```


## Job
The Job Controller ensures one or more Pods are executed and successfully terminate. Essentially a task executor that can be run in parallel.


## Lab 5 : Job
- Create a Kubernetes Job and work to understand how the Pods are managed with completions and parallelism directives.
- Create job job-example
- Watch the Pods
- Delete the job
```
kubectl create -f manifests/job-example.yaml
kubectl get pods --show-labels --watch
kubectl describe job job-example
kubectl delete job job-example
kubectl get pods
```

##  CronJob

CronJobs are an extension of the Job Controller, and enable Jobs to be run on a schedule.

## Lab 6 : CronJob
- Create a CronJob based off a Job Template. Understand how the Jobs are generated and how to suspend a job in the event of a problem.
- Create CronJob cronjob-example using the cron schedule "*/1 * * * *"
- Watch the Pods

```
kubectl create -f manifests/cronjob-example.yaml
kubectl get jobs
kubectl get jobs
kubectl describe CronJob cronjob-example
kubectl delete cronjob cronjob-example
```


## Clean up

```
kubectl delete -f manifests/

```