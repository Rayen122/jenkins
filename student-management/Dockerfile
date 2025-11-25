# IMAGE DE BASE LÉGÈRE (≈ 84 MB)
FROM amazoncorretto:17-alpine

# Dossier de travail
WORKDIR /app

# Copier le JAR généré par Maven
COPY target/student-management-0.0.1-SNAPSHOT.jar app.jar

# Lancement de l'application
CMD ["java", "-jar", "app.jar"]
