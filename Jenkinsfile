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
                sh 'mvn clean package deploy -DmuleDeploy -DskipTests -DaltDeploymentRepository=myinternalrepo::default::file:///C:/snapshots'
            }
        }
    }
    post {
        failure {
            echo 'Build or deployment failed.'
        }
    }
}
