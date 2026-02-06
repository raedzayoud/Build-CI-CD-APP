# Build stage
FROM maven:3.9.4-eclipse-temurin-17 AS build

WORKDIR /build
COPY pom.xml .
RUN mvn dependency:go-offline
COPY src ./src
RUN mvn clean package -DskipTests

# Runtime stage
FROM amazoncorretto:17

ARG PROFILE=dev
WORKDIR /app
COPY --from=build /build/target/*.jar /app/app.jar

EXPOSE 8088

ENV SPRING_DATASOURCE_URL=jdbc:postgresql://postgres-db:5432/jira
ENV SPRING_DATASOURCE_USERNAME=postgres
ENV SPRING_DATASOURCE_PASSWORD=admin
ENV SPRING_PROFILES_ACTIVE=${PROFILE}

CMD ["java", "-jar", "/app/app.jar"]
