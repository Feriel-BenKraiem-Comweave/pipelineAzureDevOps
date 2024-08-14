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
                    def branchName = sh(script: 'git for-each-ref --sort=-committerdate --format='%(refname:short)' refs/heads/ | head -n 1', returnStdout: true).trim()
                    
                    echo "Branch Name: ${branchName}"
                    
                    if (branchName == 'developer') {
                        deployEnv = 'Develop'
                    } else if (branchName == 'staging') {
                        deployEnv = 'Staging'
                    } else if (branchName == 'product') {
                        deployEnv = 'Product'
                    }

                    // Deploy only if a known environment is set
                    if (deployEnv != 'Unknown') {
                        sh "mvn -X deploy -DmuleDeploy -DskipTests -Denvironment=${deployEnv}"
                    } else {
                        echo "Branch ${branchName} does not match any known environment."
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
