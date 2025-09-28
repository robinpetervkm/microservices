# Build Stage
FROM maven:3-amazoncorretto-21 AS builder
WORKDIR /app
COPY pom.xml .
RUN mvn dependency:go-offline
COPY src ./src
RUN mvn clean package -DskipTests

# Runtime Stage
FROM openjdk:21-jdk-slim
#Information around who maintains the image
LABEL "org.opencontainers.image.authors"="eazybytes.com"
WORKDIR /app
COPY --from=builder /app/target/accounts-0.0.1-SNAPSHOT.jar accounts-0.0.1-SNAPSHOT.jar
ENTRYPOINT ["java", "-jar", "accounts-0.0.1-SNAPSHOT.jar"]
