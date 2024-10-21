[//]: # (Confidential document)
[//]: # (01/07/2023)
[//]: # (v 1.5.0)


# Kubernetes Fundamentals labs v1.5.0 - Examples 

The Examples here are fully functional applications with descriptions of their components and instructions on how they should be deployed. It is encouraged to fully explore all the manifests to gain a greater understanding of how these components work together.


## Project 1 : WordPress 


WordPress is a commonly used Blog and CMS engine that serves as an excellent introduction to a multi-tier application.

The WordPress example has two major components: A MySQL database to serve as the backing datastore and the WordPress container itself that combines the Apache webserver along with PHP and the needed application dependencies to run an instance of the blog engine.

- deploy wordpess
- access to the wordpress site
 
```
kubectl create -f manifests/ 
kubectl get pods
kubectl get secrets
kubectl get svc
kubectl port-forward --address 0.0.0.0 svc/wordpress 8888:80

```

## Clean up

```
kubectl delete -f manifests/
kubectl delete pvc mysql-data-mysql-0

```