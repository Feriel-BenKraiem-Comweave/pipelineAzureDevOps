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
        stage('Deploy CloudHubs') { 
            environment { 
                ANYPOINT_CREDENTIALS = credentials(' anypointplatformcredentials ') 
            } 
            steps { 
                sh 'mvn clean deploy -DmuleDeploy  -Dusername=${ANYPOINT_CREDENTIALS_USR} -Dpassword=${ANYPOINT_CREDENTIALS_PSW} -DworkerType=Micro -Dworkers=1' 
            }  
       } 
    }
}
