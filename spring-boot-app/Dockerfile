# Stage 1: Build the spring-boot-app using Maven with Java 8
FROM maven:3.8.5-openjdk-8-slim AS builder
WORKDIR /build
# Install git to clone the repository
RUN apt-get update && apt-get install -y git
# Clone the repository (do not fork, just clone)
RUN git clone https://github.com/kkenan/basic-microservices.git .
# Change directory to the spring-boot-app folder
WORKDIR /build/spring-boot-app
# Build the application with Maven (skip tests for a faster build)
RUN mvn clean package -DskipTests

# Stage 2: Create the final runtime image using Java 8
FROM openjdk:8-jre-slim
WORKDIR /
# Copy the built jar from the builder stage (assumes one jar is produced in target)
COPY --from=builder /build/spring-boot-app/target/*.jar /app.jar
# Expose the application port
EXPOSE 8080
# Run the application
ENTRYPOINT ["java", "-jar", "/app.jar"]
