pipeline {
    agent any
    tools {
        maven 'maven'
    }
    environment {
        CLOUDHUB_URI = 'https://anypoint.mulesoft.com/'
        MULE_VERSION = '4.7.0'
        CLOUDHUB_USERNAME = 'Feriel'
        CLOUDHUB_PASSWORD = 'Feriel123**'
        APPLICATION_NAME = 'projectcicd'
        BUSINESS_GROUP = 'ITMMA'
        ENVIRONMENT = 'Sandbox'
        WORKERS = '1'
        OBJECT_STORE_V2 = 'true'
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
                mvn org.mule.tools.maven:mule-maven-plugin:deploy \
                -DmuleDeploy \
                -DskipTests \
                -Danypoint.platform.username=${CLOUDHUB_USERNAME} \
                -Danypoint.platform.password=${CLOUDHUB_PASSWORD} \
                -Dmule.version=${MULE_VERSION} \
                -Dcloudhub.uri=${CLOUDHUB_URI} \
                -Dapplication.name=${APPLICATION_NAME} \
                -Dapplication.businessGroup=${BUSINESS_GROUP} \
                -Dapplication.environment=${ENVIRONMENT} \
                -Dapplication.workers=${WORKERS} \
                -Dapplication.objectStoreV2=${OBJECT_STORE_V2} \
                -DcloudHubDeployment="<cloudHubDeployment>\
                    <uri>${CLOUDHUB_URI}</uri>\
                    <muleVersion>${MULE_VERSION}</muleVersion>\
                    <username>${CLOUDHUB_USERNAME}</username>\
                    <password>${CLOUDHUB_PASSWORD}</password>\
                    <applicationName>${APPLICATION_NAME}</applicationName>\
                    <businessGroup>${BUSINESS_GROUP}</businessGroup>\
                    <environment>${ENVIRONMENT}</environment>\
                    <workers>${WORKERS}</workers>\
                    <objectStoreV2>${OBJECT_STORE_V2}</objectStoreV2>\
                </cloudHubDeployment>"
                '''
            }
        }
    }
    post {
        failure {
            echo 'Build or deployment failed.'
        }
    }
}
