[//]: # (Confidential document)
[//]: # (01/07/2023)
[//]: # (v 1.5.0)


# Kubernetes Fundamentals labs v1.5.0 - Configuration

Kubernetes has an integrated pattern for decoupling configuration from application or container. This pattern makes use of two Kubernetes components: ConfigMaps and Secrets.

A ConfigMap is externalized data stored within Kubernetes that can be referenced through several different means:

- Environment variable
- A command line argument (via env var)
- Injected as a file into a volume mount

ConfigMaps can be created from a manifest, literals, a directory, or from the files the directly.


A Secret is externalized "private" base64 encoded data stored within Kubernetes that can be referenced through several different means:

- Environment variable
- A command line argument (via env var)
- Injected as a file into a volume mount

Like ConfigMaps, Secrets can be created from a manifest, literals, or from files directly

## Lab 1 : ConfigMap 


There are four primary methods of creating ConfigMaps with kubectl. From a manifest, passing literals on the command-line, supplying a path to a directory, or to the individual files themselves. These ConfigMaps are stored within etcd, and may be used in a multitude of ways.


Items within a ConfigMap can be injected into a Pod's Environment Variables at container creation. These items may be picked up by the application being run in the container directly, or referenced as a command-line argument. Both methods are commonly used and enable a wide-variety of use-cases.


In addition to being injected as Environment Variables it's possible to mount the contents of a ConfigMap as a volume. This same method may be augmented to mount specific items from a ConfigMap instead of the entire thing. These items can be renamed or be made read-only to meet a variety of application needs providing an easy to use avenue to further decouple application from configuration.


 - Create ConfigMaps from manifest, literal, directory and file
 - Use ConfigMaps with Environment Variables
 - Use ConfigMaps with Volumes
 
```
kubectl create -f manifests/cm-manifest.yaml
kubectl get configmap manifest-example -o yaml

kubectl create cm literal-example --from-literal="city=Ann Arbor" --from-literal=state=Michigan
kubectl get cm literal-example -o yaml

kubectl create cm dir-example --from-file=manifests/cm/
kubectl get cm dir-example -o yaml

kubectl create cm file-example --from-file=manifests/cm/city --from-file=manifests/cm/state
kubectl get cm file-example -o yaml


kubectl create -f manifests/cm-env-example.yaml
kubectl get pods
kubectl logs cm-env-example-<pod-id>

kubectl create -f manifests/cm-cmd-example.yaml
kubectl get pods
kubectl logs cm-cmd-example-<pod-id>

kubectl delete job cm-env-example cm-cmd-example

kubectl create -f manifests/cm-vol-example.yaml
kubectl exec cm-vol-example -- ls /myconfig
kubectl exec cm-vol-example -- /bin/sh -c "cat /myconfig/*"
kubectl exec cm-vol-example -- ls /mycity
kubectl exec cm-vol-example -- cat /mycity/thisismycity

kubectl delete pod cm-vol-example
kubectl delete cm dir-example file-example literal-example manifest-example

```

## Lab 2 : Secrets

Secrets are created and used just like ConfigMaps. If you have completed the ConfigMap Exercises, the Secrets section may be skimmed over glossing a few of the minor syntax differences.

Note the Secret has the additional attribute type when compared to a ConfigMap. The Opaque value simply means the data is unstructured. Additionally, the content referenced in data itself is base64 encoded. Decoded, they are username=example and password=mypassword.


 - Create Secrets from manifest, literal, directory and file
 - Use Secrets with Environment Variables
 - Use Secrets with Volumes
 
```

kubectl create -f manifests/secret-manifest.yaml
kubectl get secret manifest-example -o yaml

 kubectl create secret generic literal-example --from-literal=username=example --from-literal=password=mypassword
kubectl get secret literal-example -o yaml

kubectl create secret generic dir-example --from-file=manifests/secret/
kubectl get secret dir-example -o yaml

kubectl create secret generic  file-example --from-file=manifests/secret/username --from-file=manifests/secret/password
kubectl get secret file-example -o yaml

kubectl create -f manifests/secret-env-example.yaml
kubectl get pods
kubectl logs secret-env-example-<pod-id>
kubectl create -f manifests/secret-cmd-example.yaml
kubectl get pods
kubectl logs secret-cmd-example-<pod-id>

kubectl delete job secret-env-example secret-cmd-example

kubectl create -f manifests/secret-vol-example.yaml
kubectl exec secret-vol-example -- ls /mysecret
kubectl exec secret-vol-example -- /bin/sh -c "cat /mysecret/*"
kubectl exec secret-vol-example -- ls /mypass
kubectl exec secret-vol-example -- cat /mypass/supersecretpass

kubectl delete pod secret-vol-example
kubectl delete secret dir-example file-example literal-example manifest-example

```


## Clean up

```
kubectl delete -f manifests/

```