# Use a base image with JDK
FROM maven:3.9.8-eclipse-temurin-21 AS build

# Set the working directory in the container
WORKDIR /app

# Copy the Maven build file
COPY pom.xml .
COPY src ./src

# Build the application (skip tests)
RUN mvn clean package -DskipTests

# Stage 2: Run the application with a slim OpenJDK image
FROM openjdk:21-jdk-slim

WORKDIR /app

# Copy the JAR file from the build stage
COPY --from=build /app/target/*.jar app.jar

# Expose the application port
EXPOSE 8080

# Run the Spring Boot application
ENTRYPOINT ["java", "-jar", "app.jar"]