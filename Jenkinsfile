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
                sh 'mvn -X deploy -DmuleDeploy -DskipTests'
            }
        }
    }
    post {
        failure {
            echo 'Build or deployment failed.'
        }
    }
}