pipeline {
    agent any

    tools {
        maven 'maven3'
    }

    environment {
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
                dir('jenkins/student-management') {
                    echo "Building Maven project inside jenkins/student-management"
                    sh "mvn clean package -DskipTests"
                }
            }
        }

        stage('Build Docker Image') {
            steps {
                dir('jenkins/student-management') {
                    echo "Building Docker image..."
                    sh "docker build -t ${IMAGE_NAME}:latest ."
                }
            }
        }

        stage('Docker Login & Push') {
            steps {
                // safer credential usage
                withCredentials([usernamePassword(credentialsId: 'dockerhub-cred22', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                    sh 'echo "$DOCKER_PASS" | docker login -u "$DOCKER_USER" --password-stdin'
                }
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
