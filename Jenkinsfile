pipeline {
    agent any

    triggers {
        pollSCM('H/2 * * * *')  
        // Toutes les 2 minutes, Jenkins vérifie GitHub
    }

    stages {
        stage('Build') {
            steps {
                echo "🚀 Pipeline lancé automatiquement via Poll SCM !"
                echo"hhhhhhhhhhh"
                echo"test"
            }
        }
    }
}
