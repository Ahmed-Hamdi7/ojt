FROM maven:3.9.12-eclipse-temurin-17-alpine
WORKDIR /build1 
COPY . . 
RUN mvn package
CMD ["java","-jar","target/demo-0.0.1-SNAPSHOT.jar"]
EXPOSE 8080
