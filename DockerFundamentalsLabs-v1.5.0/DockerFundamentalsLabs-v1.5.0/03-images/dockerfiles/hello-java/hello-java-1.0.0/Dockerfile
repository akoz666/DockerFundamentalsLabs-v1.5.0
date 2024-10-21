FROM maven:3.9.2-amazoncorretto-8-debian  AS build
RUN mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=my-app -DarchetypeArtifactId=maven-archetype-quickstart -DarchetypeVersion=1.4 -DinteractiveMode=false
WORKDIR   my-app  
RUN mvn package
ENTRYPOINT ["java", "-cp", "target/my-app-1.0-SNAPSHOT.jar ", "com.mycompany.app.App"]