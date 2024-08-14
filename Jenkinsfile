pipeline {
    agent any
    tools {
        maven 'maven'
    }
    stages {
        stage('Checkout') {
            steps {
                script {
                    checkout scm
                }
            }
        }
        
        stage('Build') {
            steps {
                script {
                    sh 'mvn clean package'
                }
            }
        }
        stage('Deploy To CloudHub') {
            steps {
                script {
                    def deployEnv = 'Unknown'
                    
                    // Determine the deployment environment based on the branch name
                    if (env.BRANCH_NAME == 'developer') {
                        deployEnv = 'Develop'
                    } else if (env.BRANCH_NAME == 'staging') {
                        deployEnv = 'Staging'
                    } else if (env.BRANCH_NAME == 'product') {
                        deployEnv = 'Product'
                    }

                    // Deploy only if a known environment is set
                    if (deployEnv != 'Unknown') {
                        sh "mvn -X deploy -DmuleDeploy -DskipTests -Denvironment=${deployEnv}"
                    } else {
                        echo "Branch ${env.BRANCH_NAME} does not match any known environment."
                    }
                }
            }
        }
    }
    post {
        failure {
            echo 'Build or deployment failed.'
        }
    }
}
