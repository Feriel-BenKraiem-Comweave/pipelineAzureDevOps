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
            steps { 
                sh 'mvn -X clean deploy -DmuleDeploy  -Dusername=998ddb532fcb48a3bd312ba779c3a64f -Dpassword=FCfA351a4405403Ca7C74dAE1F45a321 -DworkerType=Micro -Dworkers=1' 
            }  
       } 
    }
}
