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
                     ${tool 'maven'}/bin/mvn clean package

                }
            }
        }
    }
}
