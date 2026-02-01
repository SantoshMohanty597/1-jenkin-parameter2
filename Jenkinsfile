pipeline {
    agent any

    parameters {
        choice(
            name: 'ENVIRONMENT',
            choices: ['dev', 'qa', 'prod'],
            description: 'Target environment'
        )
    }

    stages {

        stage('Checkout') {
            steps {
                echo "Checking out source code"
            }
        }

        stage('Build') {
            steps {
                echo "Building application for ${params.ENVIRONMENT}"
            }
        }

        stage('Test') {
            steps {
                echo "Running tests for ${params.ENVIRONMENT}"
            }
        }

        /* ---------- DEV DEPLOY ---------- */
        stage('Deploy to DEV') {
            when {
                expression { params.ENVIRONMENT == 'dev' }
            }
            steps {
                echo "Deploying to DEV environment"
                build job: 'app-qa-para',
                parameters: [
                    string(name: 'ENVIRONMENT', value: 'qa')
                ],
                wait: false
            }
        }

        /* ---------- QA DEPLOY ---------- */
        stage('Deploy to QA') {
            when {
                expression { params.ENVIRONMENT == 'qa' }
            }
            steps {
                echo "Deploying to QA environment"
                build job: 'app-prod-para',
              parameters: [
                  string(name: 'ENVIRONMENT', value: 'prod')
              ],
              wait: false
            }
        }

        /* ---------- PROD APPROVAL ---------- */
        stage('Approve PROD Deployment') {
            when {
                expression { params.ENVIRONMENT == 'prod' }
            }
            steps {
                input message: 'Approve deployment to PRODUCTION?', ok: 'Deploy'
            }
        }

        /* ---------- PROD DEPLOY ---------- */
        stage('Deploy to PROD') {
            when {
                expression { params.ENVIRONMENT == 'prod' }
            }
            steps {
                echo "Deploying to PROD environment"
            }
        }
    }

    post {
        success {
            echo "Pipeline completed successfully for ${params.ENVIRONMENT}"
        }
        failure {
            echo "Pipeline failed for ${params.ENVIRONMENT}"
        }
    }
}
