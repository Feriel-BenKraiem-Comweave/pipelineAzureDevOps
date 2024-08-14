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
                // Dynamically inject the mule-maven-plugin configuration and deploy
                sh '''
                mvn org.apache.maven.plugins:maven-antrun-plugin:run@deploy \
                -DcloudHubUri=https://anypoint.mulesoft.com/ \
                -DmuleVersion=4.7.0 \
                -DcloudHubUsername=Feriel \
                -DcloudHubPassword=Feriel123** \
                -DcloudHubAppName=projectcicd \
                -DcloudHubBusinessGroup=ITMMA \
                -DcloudHubEnvironment=Sandbox \
                -DcloudHubWorkers=1 \
                -DcloudHubObjectStoreV2=true \
                -DcloudHubDeploymentConfig="\
                <configuration>\
                    <cloudHubDeployment>\
                        <uri>${cloudHubUri}</uri>\
                        <muleVersion>${muleVersion}</muleVersion>\
                        <username>${cloudHubUsername}</username>\
                        <password>${cloudHubPassword}</password>\
                        <applicationName>${cloudHubAppName}</applicationName>\
                        <businessGroup>${cloudHubBusinessGroup}</businessGroup>\
                        <environment>${cloudHubEnvironment}</environment>\
                        <workers>${cloudHubWorkers}</workers>\
                        <objectStoreV2>${cloudHubObjectStoreV2}</objectStoreV2>\
                    </cloudHubDeployment>\
                </configuration>" \
                -Dexec.executable="mvn" \
                -Dexec.args="org.mule.tools.maven:mule-maven-plugin:deploy -DmuleDeploy -DskipTests -DcloudHubDeploymentConfig='${cloudHubDeploymentConfig}'"
                '''
            }
        }
    }
}
