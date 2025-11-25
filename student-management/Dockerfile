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
                dir('student-management') {
                    echo "Building Maven project inside student-management folder"
                    sh "mvn clean package -DskipTests"
                }
            }
        }

        stage('Build Docker Image') {
            steps {
                dir('student-management') {
                    echo "Building Docker image..."
                    sh "docker build -t ${IMAGE_NAME}:latest ."
                }
            }
        }

        stage('Docker Login') {
            steps {
                echo "Logging into Docker Hub..."
                sh """
                    echo ${DOCKERHUB_CREDENTIALS_PSW} | docker login -u ${DOCKERHUB_CREDENTIALS_USR} --password-stdin
                """
            }
        }

        stage('Push Image') {
            steps {
                echo "Pushing Docker image to Docker Hub..."
                sh "docker tag ${IMAGE_NAME}:latest ${DOCKERHUB_REPO}:latest"
                sh "docker push ${DOCKERHUB_REPO}:latest"
            }
        }
    }

    post {
        success { echo "Pipeline completed successfully!" }
        failure { echo "Pipeline failed!" }
    }
}
