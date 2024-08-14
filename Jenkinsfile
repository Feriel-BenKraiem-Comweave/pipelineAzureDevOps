node {
    def deployEnv = 'Unknown'

    // Checkout code
    stage('Checkout') {
        checkout scm
    }

    // Build the project
    stage('Build') {
        sh 'mvn clean package'
    }

    // Determine the environment and deploy
    stage('Deploy To CloudHub') {
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
    
    // Post-build actions
    post {
        failure {
            echo 'Build or deployment failed.'
        }
    }
}