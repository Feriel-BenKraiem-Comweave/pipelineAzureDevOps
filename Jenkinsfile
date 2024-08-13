pipeline {
    agent any
    tools {
        maven 'maven'
    }
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }
        stage('Deploy To CloudHub') {
            steps {
                sh 'mvn deploy -Danypoint.clientId=998ddb532fcb48a3bd312ba779c3a64f -Danypoint.clientSecret=FCfA351a4405403Ca7C74dAE1F45a321'
            }
        }
    }
    post {
        failure {
            echo 'Build or deployment failed.'
        }
    }
}
