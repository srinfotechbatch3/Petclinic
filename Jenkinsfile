pipeline {
    agent any

    stages {
        stage('Clone') {
            steps {
               git branch: 'feature/2025.08.21', url: 'https://github.com/srinfotechbatch3/Petclinic.git'
            }
        }

        stage('Build') {
            steps {
               bat 'mvn clean install'
            }
        }

        stage('Test') {
            steps {
               bat 'mvn test'
            }
        }

         stage('Test reports') {
            steps {
               junit 'target/surefire-reports/*.xml'
            }
        }

        stage('Published Artifacts') {
            steps {
              archiveArtifacts artifacts: 'target/*.war', followSymlinks: false
            }
        }

        stage('Deploy to Target Server') {
            steps {
              deploy adapters: [tomcat9(alternativeDeploymentContext: '', credentialsId: 'TomcatCredentials', path: '', url: 'http://localhost:8080/')], contextPath: 'SRINFOTECHSpringPetclinic', war: 'target/*.war'
            }
        }
		
    }
}
