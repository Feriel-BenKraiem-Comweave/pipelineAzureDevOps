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
                sh 'mvn -X clean deploy -DmuleDeploy  -Dusername=998ddb532fcb48a3bd312ba779c3a64f -Dpassword=998ddb532fcb48a3bd312ba779c3a64f -DworkerType=Micro -Dworkers=1' 
            }  
       } 
    }
}
