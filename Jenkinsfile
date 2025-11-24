pipeline {
    agent any

    triggers {
        githubPush()   // Déclenche automatiquement à chaque push GitHub
    }

    stages {
        stage('Build') {
            steps {
                echo "🔥 Pipeline lancé automatiquement après un commit !"
                echo "➡️ Construction du projet..."
                echo "Pipeline lancé automatiquement"

            }
        }

        stage('Tests') {
            steps {
                echo "🧪 Exécution des tests..."
            }
        }

        stage('Deploy') {
            steps {
                echo "🚀 Déploiement terminé."
            }
        }
    }
}

