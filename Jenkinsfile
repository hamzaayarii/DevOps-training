pipeline {
    agent any

    environment {
        MAVEN_HOME = '/usr/share/maven' // Adapt if needed
    }

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/hamza10tn/atelier-git.git'
            }
        }

        stage('Build') {
            steps {
                sh 'echo "Building the project..."'
                sh 'mvn clean compile'
            }
        }

        stage('Test') {
            steps {
                sh 'echo "Running tests..."'
                sh 'mvn test'
            }
        }

        stage('Package') {
            steps {
                sh 'echo "Packaging the application..."'
                sh 'mvn package'
            }
        }

        stage('Deploy') {
            when {
                branch 'main'
            }
            steps {
                sh 'echo "Deploying the application..."'
                // Example for copying the JAR somewhere
                // sh 'scp target/*.jar user@server:/path/to/deploy'
            }
        }
    }

    post {
        success {
            echo '✅ Build successful!'
        }
        failure {
            echo '❌ Build failed.'
        }
    }
}
