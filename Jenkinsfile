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
                    def token = sh(script: 'curl -X POST https://anypoint.mulesoft.com/accounts/api/v2/oauth2/token -d "grant_type=client_credentials&client_id=998ddb532fcb48a3bd312ba779c3a64f&client_secret=FCfA351a4405403Ca7C74dAE1F45a321" -H "Content-Type: application/x-www-form-urlencoded" | jq -r .access_token', returnStdout: true).trim()
                    sh "mvn clean deploy -DmuleDeploy -Dusername=Feriel -Dpassword=${token} -DworkerType=Micro -Dworkers=1"
                }
            }
   }
}