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
        stage('Modify pom.xml') {
            steps {
                script {
                    def pomFile = readFile('pom.xml')
                    def newConfiguration = """
                    <configuration>
                        <cloudHubDeployment>
                            <uri>${CLOUDHUB_URI}</uri>
                            <muleVersion>${MULE_VERSION}</muleVersion>
                            <username>${CLOUDHUB_USERNAME}</username>
                            <password>${CLOUDHUB_PASSWORD}</password>
                            <applicationName>${APPLICATION_NAME}</applicationName>
                            <businessGroup>${BUSINESS_GROUP}</businessGroup>
                            <environment>${ENVIRONMENT}</environment>
                            <workers>${WORKERS}</workers>
                            <objectStoreV2>${OBJECT_STORE_V2}</objectStoreV2>
                        </cloudHubDeployment>
                    </configuration>
                    """
                    def updatedPom = pomFile.replaceFirst(/(<build>[\s\S]*?<\/build>)/, "\$1${newConfiguration}")
                    writeFile(file: 'pom.xml', text: updatedPom)
                }
            }
        }
        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }
        stage('Deploy To CloudHub') {
            steps {
                sh 'mvn org.mule.tools:mule-maven-plugin:deploy -DmuleDeploy -DskipTests'
            }
        }
    }
    post {
        failure {
            echo 'Build or deployment failed.'
        }
    }
}