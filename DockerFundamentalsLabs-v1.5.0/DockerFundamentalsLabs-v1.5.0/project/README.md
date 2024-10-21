[//]: # (Confidential document)
[//]: # (01/07/2023)
[//]: # (v 1.5.0)


# Docker labs v1.5.0 - Project


## Lab 1 :Dockerfile

- Maven in 5 Minutes https://maven.apache.org/guides/getting-started/maven-in-five-minutes.html
- Create Dockerfile for java Hello World! (Java 8)

```
mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=my-app -DarchetypeArtifactId=maven-archetype-quickstart -DarchetypeVersion=1.4 -DinteractiveMode=false
cd my-app
mvn package
java -cp target/my-app-1.0-SNAPSHOT.jar com.mycompany.app.App
```
- Build & Run image

```
docker build -t hello-world-java:1.0.0 .
docker run hello-world-java:1.0.0 .
docker image ls
```


## Lab 2 : Multi-stage Dockerfile

- Create Multi-stage Dockerfile for java Hello World!
- Build & Run image
- Check image size


```
docker build -t hello-world-java:1.0.1 .
docker run hello-world-java:1.0.1 .
docker image ls
```