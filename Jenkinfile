pipeline {
    agent any

    parameters {
        choice(name: 'ENVIRONMENT', choices: ['dev', 'qa', 'prod'], description: 'Select the environment to deploy to')
    }

    stages {
        stage('Build') {
            steps {
                echo 'Building the application...'
                // Add your build commands here
            }
        }

        stage('Test') {
            steps {
                echo 'Running tests...'
                // Add your test commands here
            }
        }

        stage('Deploy') {
            steps {
                script {
                    if (params.ENVIRONMENT == 'dev') {
                        echo 'Try Commit Deploying to Development environment...'
                        // Add your deployment commands for dev here
                    } else if (params.ENVIRONMENT == 'qa') {
                        echo 'Try Commit Deploying to QA environment...'
                        // Add your deployment commands for qa here
                    } else if (params.ENVIRONMENT == 'prod') {
                        echo 'Deploying to Production environment...'
                        // Add your deployment commands for prod here
                    }
                }
            }
        }
    }

    post {
        always {
            echo 'Cleaning up...'
            // Add any cleanup commands here
        }
    }
}
