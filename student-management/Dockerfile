FROM openjdk:17.0.1-jdk-slim

WORKDIR /app

# Copier le jar (application)
COPY target/*.jar /app/app.jar

# Génération automatique d'une image ASCII dans le container
RUN echo "**********************"  > /app/photo.txt && \
    echo "*   BONJOUR RAYEN    *" >> /app/photo.txt && \
    echo "**********************" >> /app/photo.txt

EXPOSE 8089

CMD ["sh", "-c", "echo 'Voici la photo générée :' && cat /app/photo.txt && java -jar /app/app.jar"]
