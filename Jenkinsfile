pipeline {
    agent any
    tools {
        maven 'maven' 
    }
    stages {
        stage('Checkout') {
            steps {
                checkout scm  // Checkout code from the SCM configured in the Jenkins job
            }
        }
        stage('Build') {
            steps {
                sh 'mvn clean package'  // Run Maven to clean and package the code
            }
        }
        stage('Deploy To CloudHub') {
            steps {
                sh 'mvn -X deploy -DmuleDeploy -DskipTests'  // Deploy the code to CloudHub
            }
        }
    }
    post {
        failure {
            echo 'Build or deployment failed.'  // Log a message if the build or deployment fails
        }
    }
}
