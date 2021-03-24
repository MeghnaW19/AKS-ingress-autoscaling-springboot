#Dockerfile contains all the commands with which
#Docker can build images reading the instructions.

FROM openjdk:11

ADD ./target/service-app-0.0.1-SNAPSHOT.jar /usr/src/service-app-0.0.1-SNAPSHOT.jar

WORKDIR usr/src

ENTRYPOINT ["java","-jar", "service-app-0.0.1-SNAPSHOT.jar"]