pipeline {
    agent any
    environment {
        DIRECTORY_PATH = '/var/jenkins_home'
        TESTING_ENVIRONMENT = '5.1_Pipeline'
        PRODUCTION_ENVIRONMENT = 'Liana Perry'
    }
    stages {
        stage('Build') {
            steps {
                echo "Fetch the source code from the directory path specified by the environment variable: ${env.DIRECTORY_PATH}"
                echo "Compile the code and generate any necessary artifacts"
            }
        }
        stage('Test') {
            steps {
                echo "Running unit tests"
                echo "Running integration tests"
            }
        }
        stage('Code Quality Check') {
            steps {
                echo "Check the quality of the code"
            }
        }
        stage('Deploy') {
            steps {
                echo "Deploy the application to the testing environment specified by the environment variable: ${env.TESTING_ENVIRONMENT}"
            }
        }
        stage('Approval') {
            steps {
                echo "Awaiting manual approval..."
                sleep 10
            }
        }
        stage('Deploy to Production') {
            steps {
                echo "Deploy the code to the production environment: ${env.PRODUCTION_ENVIRONMENT}"
            }
        }
        post{
            success{
                mail to: "lianaperry022@gmail.com",
                subject: "Build Status"
                body: "Build was successful!"
            }
        }
    }
}
