# Étape 1 : Construction de l'application
FROM maven:3.9.9-eclipse-temurin-23-noble AS builder

# Définir le répertoire de travail
WORKDIR /app

# Copier les fichiers de configuration et de dépendances Maven/Gradle
COPY pom.xml ./
COPY src ./src

# Construire l'application
RUN mvn package -DskipTests

# Étape 2 : Image finale pour exécuter l'application
FROM amazoncorretto:23-alpine-jdk

# Définir le répertoire de travail
WORKDIR /app

# Copier le fichier JAR de l'étape précédente
COPY --from=builder /app/target/*.jar app.jar

# Exposer le port
EXPOSE 8080

# Commande pour exécuter l'application
ENTRYPOINT ["java", "-jar", "app.jar"]
