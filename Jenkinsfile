pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/Rayen122/jenkins.git'
            }
        }

        stage('Build') {
            steps {
                echo 'Compilation du projet...'
            }
        }

        stage('Tests') {
            steps {
                echo 'Exécution des tests...'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Déploiement terminé !'
            }
        }
    }
}
