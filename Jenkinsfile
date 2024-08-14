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
                sh '''
                mvn deploy -DmuleDeploy -DskipTests \
                -DcloudHubUri=https://anypoint.mulesoft.com/ \
                -DmuleVersion=4.7.0 \
                -DcloudHubUsername=Feriel \
                -DcloudHubPassword=Feriel123** \
                -DcloudHubAppName=projectcicd \
                -DcloudHubBusinessGroup=ITMMA \
                -DcloudHubEnvironment=Sandbox \
                -DcloudHubWorkers=1 \
                -DcloudHubObjectStoreV2=true
                '''
            }
        }
    }
}
