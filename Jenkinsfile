pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/user/repository.git'
            }
        }

        stage('Build') {
            steps {
                sh 'echo "Building the project..."'
                // Exemple pour un projet Node.js
                sh 'npm install'
            }
        }

        stage('Test') {
            steps {
                sh 'echo "Running tests..."'
                sh 'npm test' // Exécute les tests
            }
        }

        stage('Deploy') {
            when {
                branch 'main'
            }
            steps {
                sh 'echo "Deploying the application..."'
                // Ajoute ici les commandes de déploiement
            }
        }
    }

    post {
        always {
            echo 'Pipeline terminé.'
        }
    }
}
