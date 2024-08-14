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
        stage('Deploy To CloudHub - Develop') {
            when {
                branch 'developer'
            }
            steps {
                sh 'mvn -X deploy -DmuleDeploy -DskipTests -Denvironment=Develop'
            }
        }
        stage('Deploy To CloudHub - Test') {
            when {
                branch 'staging'
            }
            steps {
                sh 'mvn -X deploy -DmuleDeploy -DskipTests -Denvironment=Staging'
            }
        }
        stage('Deploy To CloudHub - Production') {
            when {
                branch 'product'
            }
            steps {
                sh 'mvn -X deploy -DmuleDeploy -DskipTests -Denvironment=Product'
            }
        }        
    }
    post {
        failure {
            echo 'Build or deployment failed.'
        }
    }
}