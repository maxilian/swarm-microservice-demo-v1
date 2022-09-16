#FROM java:8
FROM openjdk:11

RUN apt-get update -qq && apt-get install -y maven && apt-get clean

WORKDIR /code

ADD pom.xml /code/pom.xml
RUN ["mvn", "dependency:resolve"]
#RUN ["mvn", "org.apache.maven.plugins:maven-resources-plugin:2.3:tree", "-Dverbose=true"]

RUN ["mvn", "verify"]

# Adding source, compile and package into a fat jar
ADD src /code/src
RUN ["mvn", "package"]

CMD ["/usr/lib/jvm/java-11-openjdk-amd64/bin/java", "-jar", "target/worker-jar-with-dependencies.jar"]
