[//]: # (Confidential document)
[//]: # (01/07/2023)
[//]: # (v 1.5.0)


# Docker labs v1.5.0 - Containers


Docker is an open platform for developing, shipping, and running applications.

Docker allows you to separate your applications from your infrastructure so you can deliver software quickly. With Docker, you can manage your infrastructure in the same ways you manage your applications.

Get Docker : https://docs.docker.com/get-docker/

A container is an isolated environment for your code. This means that a container has no knowledge of your operating system, or your files.

## Lab 1 : Hello Docker CLI

- Docker CLI

```
docker 
docker container --help 
docker version
docker info

docker run hello-world
```

## Lab 2 : Running Containers

- Run Containers
- List Containers
- Inspect Containers

```
docker container rm -f $(docker container ls -aq)

docker container run centos:7 echo "hello world"
docker container run centos:7 ps aux
docker container ls
docker container ls –a
docker container inspect {id-of-container}
```


## Lab 3 : Start and Stop

- Run Containers
- Stop Containers
- Start Containers

```
docker container rm -f $(docker container ls -aq)

docker container run -d centos:7 ping 127.0.0.1
docker container ls
docker container stop {id-of-container}
docker container ls
docker container start -a {id-of-container}
```

## Lab 4 : Detached vs Interactive

- Run Containers
- Test write operation

``` 
docker container rm -f $(docker container ls -aq)
docker container run -it centos:7 bash
	# echo 'Hello Docker...' > docker.txt
	# ls -l
	# exit
docker container run -it centos:7 bash
	# ls -l
docker container ls -a
docker container start {id-of-container}
docker container exec -it {id-of-container} bash
	# ls -l
docker container ls -a
``` 

## Lab 5 : Detached Containers

- Run Containers
- Use Logging Options

``` 
docker container rm -f $(docker container ls -aq)

docker container run centos:7 ping 127.0.0.1
docker container run -d centos:7 ping 127.0.0.1
docker container logs {id-of-container}
docker container logs -f {id-of-container}
``` 

## Lab 6 : System

- System details
- System prune

``` 
docker system info
docker system events


docker system df
docker system prune
#docker image|container|volume |network prune  [-- filter 'env=dev']
``` 