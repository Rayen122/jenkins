pipeline {
    agent any

    tools {
        maven 'maven3'
    }

    environment {
        DOCKERHUB_CREDENTIALS = credentials('dockerhub-cred22')
        DOCKERHUB_REPO = "rayen122/student-management"
        IMAGE_NAME = "student-management"
    }

    stages {

        stage('Checkout') {
            steps {
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
                sh "docker build -t ${IMAGE_NAME}:latest ."
            }
        }

        stage('Login DockerHub') {
            steps {
                sh """
                    echo ${DOCKERHUB_CREDENTIALS_PSW} | \
                    docker login -u ${DOCKERHUB_CREDENTIALS_USR} --password-stdin
                """
            }
        }

        stage('Push Image') {
            steps {
                sh "docker tag ${IMAGE_NAME}:latest ${DOCKERHUB_REPO}:latest"
                sh "docker push ${DOCKERHUB_REPO}:latest"
            }
        }
    }
}
