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
                script {
                    sh "mvn clean deploy -DmuleDeploy -Dusername=Feriel -Dpassword=e11b7399-2268-4a87-bf01-5779ecbe078c -DworkerType=Micro -Dworkers=1"
                }
            }
       }     
   }
}