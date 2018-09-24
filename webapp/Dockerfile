//FROM openjdk

//COPY target/webapp-1.0-SNAPSHOT-jar-with-dependencies.jar /opt/webapp-1.0-SNAPSHOT-jar-with-dependencies.jar

//CMD java -jar /opt/webapp-1.0-SNAPSHOT-jar-with-dependencies.jar

FROM openjdk:7
COPY . /usr/src/main/java/org/example
WORKDIR /usr/src/main/java/org/example
RUN javac Main.java
CMD ["java", "Main"]
