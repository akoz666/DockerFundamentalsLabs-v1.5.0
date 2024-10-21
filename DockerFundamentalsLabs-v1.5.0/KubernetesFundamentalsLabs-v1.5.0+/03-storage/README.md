[//]: # (Confidential document)
[//]: # (01/07/2023)
[//]: # (v 1.5.0)


# Kubernetes Fundamentals labs v1.5.0 - Storage

Volumes within Kubernetes are storage that is tied to the Pod’s lifecycle.
A pod can have one or more type of volumes attached to it. These volumes are consumable by any of the containers within the pod.
They can survive Pod restarts; however their durability beyond that is dependent on the Volume Type.


Persistent Volumes and Claims work in conjunction to serve as the direct method in which a Pod Consumes Persistent storage.
A PersistentVolume (PV) is a representation of a cluster-wide storage resource that is linked to a backing storage provider - NFS, GCEPersistentDisk, RBD etc.
A PersistentVolumeClaim acts as a namespaced request for storage that satisfies a set of a requirements instead of mapping to the storage resource directly.
This separation of PV and PVC ensures that an application’s ‘claim’ for storage is portable across numerous backends or providers.


Storage classes are an abstraction on top of an external storage resource (PV). They work directly with the external storage system to enable dynamic provisioning and remove the need for the cluster admin to pre-provision Persistent Volumes.


## Lab 1 : Volumes 

Pods may have multiple volumes using different Volume types. Those volumes in turn can be mounted to one or more containers within the Pod by adding them to the volumeMounts list. This is done by referencing their name and supplying their mountPath. Additionally, volumes may be mounted both read-write or read-only depending on the application, enabling a variety of use-cases.

Understand how to add and reference volumes to a Pod and their containers.
 - Create a Pod with emptydir volume
 - check read only option
 
```
kubectl create -f manifests/volume-example.yaml
kubectl exec volume-example -c content -- /bin/sh -c "cat /html/index.html"
kubectl exec volume-example -c nginx -- /bin/sh -c "cat /usr/share/nginx/html/index.html"
kubectl exec volume-example -c nginx -- /bin/sh -c "echo nginx >> /usr/share/nginx/html/index.html"

```

## Lab 2 : Persistent Volumes/Storage Classes


Storage Classes provide a method of dynamically provisioning Persistent Volumes from an external Storage System. They have the same attributes as normal PVs, and have their own methods of being garbage collected. They may be targeted by name using the storageClassName within a Persistent Volume Claim request, or a Storage Class may be configured as default ensuring that Claims may be fulfilled even when there is no valid selector target.

Understand how it's possible for a Persistent Volume Claim to consume dynamically provisioned storage via a Storage Class.
 - describe Storage Class
 - create/describe Persistent Volume Claim
 - describe Persistent Volume


```
kubectl describe sc standard
kubectl create -f manifests/pvc-standard.yaml
kubectl describe pvc pvc-standard
kubectl get pv
```


## Clean up

```
kubectl delete -f manifests/

```