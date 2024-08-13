pipeline {
    agent any
    tools {
        maven 'maven' 
    }
    }
    stages {
        stage('Checkout') {
            steps {
                script {
                    checkout scm
                }
            }
        }
        stage('Build') {
            steps {
                script {
                     mvn clean package

                }
            }
        }
    }
}
