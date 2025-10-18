FROM maven:3.9.5-eclipse-temurin-17 AS build

WORKDIR /app

# Copy the entire project into the container
COPY . .

# Build the application using Maven
RUN mvn clean package -DskipTests

# JDK image
FROM eclipse-temurin:17-jdk-alpine

WORKDIR /app

# Copy the built JAR file from the build stage
COPY --from=build /app/target/*.jar app.jar

EXPOSE 8080

CMD ["java", "-Dspring.profiles.active=production-microservice","-jar", "app.jar"]
