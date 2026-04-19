# Dockerfile for Multi-Stage Spring Boot Build

# Stage 1: Build the Spring Boot application
FROM maven:3.8.6-openjdk-17 AS builder

WORKDIR /app
COPY pom.xml .
COPY src ./src

RUN mvn clean install -DskipTests

# Stage 2: Run the Spring Boot application
FROM openjdk:17-jdk-slim

WORKDIR /app
COPY --from=builder /app/target/*.jar app.jar

# Expose the application's port
EXPOSE 8080

# Command to run the application
ENTRYPOINT ["java", "-jar", "app.jar"]