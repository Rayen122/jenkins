FROM openjdk:17.0.1-jdk-slim

WORKDIR /app

# Installer ImageMagick pour générer une image
RUN apt-get update && apt-get install -y imagemagick

# Générer automatiquement une image
RUN convert -size 600x400 xc:lightblue -gravity center \
     -pointsize 28 -annotate 0 "Image générée automatiquement" /app/generated.jpg

COPY target/*.jar /app.jar

EXPOSE 8089

ENTRYPOINT ["java", "-jar", "/app.jar"]
