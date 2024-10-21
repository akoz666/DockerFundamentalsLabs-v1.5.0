[//]: # (Confidential document)
[//]: # (01/07/2023)
[//]: # (v 1.5.0)


# Docker labs v1.5.0 - Resource constraints

The operator can also adjust the performance parameters of the container.


## Lab 1 : Limit a container's resources (CPU/Memory)

- Limit a container's memory
- Limit a container's CPU


```
docker run -ti --memory 100m python
docker run -ti --memory 100m --memory-swap 100m python
docker run -it --cpus=0 .5  centos:7 /bin/bash
docker run -it --cpus=0.5 --cpuset-cpus 0 centos:7 /bin/bash
```



