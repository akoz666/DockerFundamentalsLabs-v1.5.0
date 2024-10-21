[//]: # (Confidential document)
[//]: # (01/07/2023)
[//]: # (v 1.5.0)


# Docker labs v1.5.0 - Netwroks

Container networking refers to the ability for containers to connect to and communicate with each other, or to non-Docker workloads.


By default, when you create or run a container using docker create or docker run, the container doesn't expose any of its ports to the outside world. Use the --publish or -p flag to make a port available to services outside of Docker. This creates a firewall rule in the host, mapping a container port to a port on the Docker host to the outside world.



Docker's networking subsystem is pluggable, using drivers. Several drivers exist by default, and provide core networking functionality:

bridge: The default network driver. 

- host: Remove network isolation between the container and the Docker host, and use the host's networking directly. See Host network driver.

- overlay: Overlay networks connect multiple Docker daemons together and enable Swarm services and containers to communicate across nodes. This strategy removes the need to do OS-level routing. See Overlay network driver.

- ipvlan: IPvlan networks give users total control over both IPv4 and IPv6 addressing. 

- macvlan: Macvlan networks allow you to assign a MAC address to a container, making it appear as a physical device on your network. 

- none: Completely isolate a container from the host and other containers. none is not available for Swarm services. See None network driver.

- Network plugins: You can install and use third-party network plugins with Docker.



## Lab 1 : Publish Ports

- Publish or expose port automatically
- Publish or expose port manually


```
docker run -d -p 80:80 --name mynginx nginx
docker port mynginx
```

```
#49153 - 65535

docker run -d -P --name mynginxauto nginx
docker port mynginxauto
```



## Lab 2 : Create your own bridge network


- Create your own bridge network
- Run container using your own bridge
- Check connectivity

```
docker network create -d bridge my_bridge
docker network inspect my_bridge
docker container run  --net=my_bridge --name db -v db_volume:/var/lib/postgresql/data -e POSTGRES_PASSWORD=mysecretpassword -d postgres:9.4-alpine
docker inspect --format='{{json .NetworkSettings.Networks}}'  db
docker inspect --format='{{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}' db
docker run -d --name web centos:7 ping 127.0.0.1
docker inspect --format='{{json .NetworkSettings.Networks}}'  web
docker inspect --format='{{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}' web
docker container exec -it db bash
	# ping ip-web-container
	# exit
docker network connect my_bridge web
docker inspect --format='{{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}' web
docker container exec -it db bash
	# ping web
```