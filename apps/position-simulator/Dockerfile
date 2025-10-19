FROM maven:3.9.5-eclipse-temurin-17 AS build

# Set the working directory inside the container
WORKDIR /app

# Copy the entire project into the container
COPY . .

# Build the application using Maven
RUN mvn clean package -DskipTests

# Use a lightweight JDK image for the runtime stage
FROM eclipse-temurin:17-jdk-alpine

# Set the working directory for the runtime stage
WORKDIR /app

# Copy the built JAR file from the build stage
COPY --from=build /app/target/*.jar app.jar

# Run the application
CMD ["java", "-Dspring.profiles.active=production-microservice","-jar", "app.jar"]
