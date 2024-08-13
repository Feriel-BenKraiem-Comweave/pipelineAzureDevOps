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
                sh 'mvn clean deploy -DmuleDeploy  -Dusername=Feriel -Dpassword=Feriel123** -DworkerType=Micro -Dworkers=1' 
            }  
       } 
    }
}
