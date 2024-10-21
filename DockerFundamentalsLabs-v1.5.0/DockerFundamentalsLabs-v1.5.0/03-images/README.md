[//]: # (Confidential document)
[//]: # (01/07/2023)
[//]: # (v 1.5.0)


# Docker labs v1.5.0 - Images



## Lab 1 : Create image using commit

- Run Centos image
- Install wget
- Check container diff
- Commit the diff
- Run new image and check wget

```
docker container run -it centos:7 bash
	# yum install -y wget
	# exit
docker container ls -a
docker container diff {id-of-container}
docker container commit {id-of-container} wget:1.0.0
docker image ls
docker container run -it wget:1.0.0 bash
	# wget

```

## Lab 2 : Create image using Dockerfile

- Introduction to build concepts
- Image size optimization
- Build speed performance improvements
- CMD vs ENTRYPOINT
- Multi-stage dockerfile
- Multi-platform builds

---
Dockerfile 1.0.0

```
FROM centos:7
CMD ["ping", "127.0.0.1", "-c", "10"]
```

```
docker image build -t ping:1.0.0 .
docker container run ping:1.0.0
docker container run ping:1.0.0 ps -ef
```
---
Dockerfile 1.0.1

```
FROM centos:7
ENTRYPOINT ["ping", "-c", "10"]
CMD ["127.0.0.1"]
```

```
docker image build -t ping:1.0.1 .
docker container run ping:1.0.1
docker container run ping:1.0.1 ps -ef
docker container run ping:1.0.1 127.0.0.1
```
---
Dockerfile 1.0.2

```
FROM centos:7
ENTRYPOINT ["ping", "127.0.0.1", "-c"]
CMD ["10"]
```

```
docker image build -t ping:1.0.2 .
docker container run ping:1.0.2
docker container run ping:1.0.2 ps -ef
docker container run ping:1.0.2 127.0.0.1
docker container run ping:1.0.2 5

```

---
Hello Java Dockerfile 1.0.0

https://maven.apache.org/guides/getting-started/maven-in-five-minutes.html

```
mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=my-app -DarchetypeArtifactId=maven-archetype-quickstart -DarchetypeVersion=1.4 -DinteractiveMode=false
cd my-app
mvn package
java -cp target/my-app-1.0-SNAPSHOT.jar com.mycompany.app.App
Hello World!
```

```
docker image build -t helo-java:1.0.0 .
docker run hello-java:1.0.0
docker image ls
```

---
Hello Java Dockerfile 1.0.1

Multi-stage dockerfile

```
docker image build -t helo-java:1.0.1 .
docker run hello-java:1.0.1
docker image ls
```

## Lab 3 : Share Docker image

- Create an account https://store.docker.com
- Tag images
- Push images


```
docker image pull centos:7
docker login
docker image tag centos:7 {dockerhub-username}/centos:training
docker image push {dockerhub-username}/centos:training

```



## Lab 4 : Image layers

```
sudo apt  install jq
sudo cat /var/lib/docker/image/overlay2/repositories.json | jq

```

## Lab 5 : Harbor & Trivy

- Push images to Harbor
- Scan images using Trivy

```
docker login demo.goharbor.io -u demo -p Dem0Dem0

docker pull ubuntu
docker pull alpine
docker pull centos
docker pull node
docker pull node:lts-alpine3.14
docker pull mysql
docker pull mysql:5.6
docker pull wordpress:4.9-apache 


docker tag ubuntu demo.goharbor.io/demo/ubuntu
docker tag alpine demo.goharbor.io/demo/alpine
docker tag centos demo.goharbor.io/demo/centos
docker tag node demo.goharbor.io/demo/node
docker tag node:lts-alpine3.14 demo.goharbor.io/demo/node:lts-alpine3.14
docker tag mysql demo.goharbor.io/demo/mysql
docker tag mysql:5.6 demo.goharbor.io/demo/mysql:5.6
docker tag wordpress:4.9-apache demo.goharbor.io/demo/wordpress:4.9-apache

docker push demo.goharbor.io/demo/ubuntu
docker push demo.goharbor.io/demo/alpine
docker push demo.goharbor.io/demo/centos
docker push demo.goharbor.io/demo/node
docker push demo.goharbor.io/demo/node:lts-alpine3.14
docker push demo.goharbor.io/demo/mysql
docker push demo.goharbor.io/demo/mysql:5.6
docker push demo.goharbor.io/demo/wordpress:4.9-apache
```