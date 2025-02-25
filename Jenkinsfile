
pipeline {
    agent any

    tools { 
        jdk 'JAVA_HOME' 
        maven 'M2_HOME' 
    }

    stages {
        stage('GIT') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/hamza10tn/atelier-git.git'
            }
        }

        stage('Compile Stage') {
            steps {
                sh 'mvn clean compile'
            }
        }
         stage('MVN SONARQUBE') {
            steps {
                script {
                    // Utilisation du token depuis Jenkins credentials
                    withCredentials([string(credentialsId: 'sonarqube-token', variable: 'SONAR_TOKEN')]) {
                        sh "mvn sonar:sonar -Dsonar.login=${SONAR_TOKEN} -Dmaven.test.skip=true"
                    }
                }
            }
         }


          stage('Deploy to Nexus') {
                     steps {
                         script {
                             // Here we use mvn deploy to upload artifacts to Nexus
                             sh """
                                 mvn deploy:deploy-file \
                                     -Dfile=target/your-artifact.jar \  # Replace with your actual artifact file
                                     -DgroupId=tn.esprit.spring.services \
                                     -DartifactId=timesheet-devops \
                                     -Dversion=1.0 \
                                     -Dpackaging=jar \
                                     -DrepositoryId=deploymentRepo \  # This matches the <id> in your settings.xml
                                     -Durl=http://192.168.33.10:8083/repository/maven-releases/ \
                                     -DgeneratePom=true
                             """
                         }
                     }
                 }

        

}
}