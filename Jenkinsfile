pipeline {
    agent any

    environment {
        DOCKERHUB_CREDENTIALS = credentials('dockerhub-cred22')

 // ID mte3 credentials dans Jenkins
        DOCKERHUB_REPO = "rayen122/student-management"        // Remplaceh b esm repository mte3ek
        IMAGE_NAME = "student-management"
    }

    triggers {
        pollSCM('H/2 * * * *')  // Vérifie GitHub chaque 2 minutes
    }

    stages {

        stage('Checkout') {
            steps {
                echo "Clonage du repository GitHub..."
                checkout scm
            }
        }

        stage('Build Maven') {
            steps {
                echo "Compilation du projet Maven..."
                sh "mvn clean package -DskipTests"
            }
        }

        stage('Build Docker Image') {
            steps {
                echo "Construction de l'image Docker..."
                sh "docker build -t ${IMAGE_NAME}:latest ."
            }
        }

        stage('Login DockerHub') {
            steps {
                echo "Connexion à Docker Hub..."
                sh """
                    echo ${DOCKERHUB_CREDENTIALS_PSW} | \
                    docker login -u ${DOCKERHUB_CREDENTIALS_USR} --password-stdin
                """
            }
        }

        stage('Tag Image') {
            steps {
                echo "Tag de l'image..."
                sh "docker tag ${IMAGE_NAME}:latest ${DOCKERHUB_REPO}:latest"
            }
        }

        stage('Push Image') {
            steps {
                echo "Push de l'image vers Docker Hub..."
                sh "docker push ${DOCKERHUB_REPO}:latest"
            }
        }
    }

    post {
        success {
            echo "Pipeline terminé avec succès 🎉"
        }
        failure {
            echo "Erreur dans le pipeline ❌"
        }
    }
}
