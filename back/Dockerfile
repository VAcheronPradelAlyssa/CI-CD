# Multi-stage build pour optimiser la taille
FROM maven:3.8.4-openjdk-11-slim AS builder

WORKDIR /app
COPY pom.xml .
RUN mvn dependency:go-offline -B

COPY src ./src
RUN mvn clean package -DskipTests

# Image de production
FROM openjdk:11-jre-slim

WORKDIR /app

# Créer un utilisateur non-root
RUN groupadd -r bobapp && useradd -r -g bobapp bobapp

# Copier le JAR depuis le stage builder
COPY --from=builder /app/target/*.jar app.jar

# Changer la propriété vers l'utilisateur bobapp
RUN chown bobapp:bobapp app.jar
USER bobapp

EXPOSE 8080

HEALTHCHECK --interval=30s --timeout=3s --start-period=40s --retries=3 \
  CMD curl -f http://localhost:8080/api/joke || exit 1

ENTRYPOINT ["java", "-jar", "app.jar"]
