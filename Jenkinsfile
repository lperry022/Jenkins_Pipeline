pipeline {
    agent any
    environment {
        DIRECTORY_PATH = '/var/jenkins_home'
        TESTING_ENVIRONMENT = '5.1_Pipeline'
        PRODUCTION_ENVIRONMENT = 'Liana Perry'
        RECIPIENT_EMAIL = 'lianaperry022@gmail.com'
    }
    stages {
        stage('Build') {
            steps {
                echo "Fetching the source code from the directory path specified by the environment variable: ${env.DIRECTORY_PATH}"
                echo "Compiling the code and generating any necessary artifacts using Maven"
                // sh 'mvn clean package'
            }
        }
        stage('Unit and Integration Tests') {
            steps {
                echo "Running unit tests using JUnit"
                echo "Running integration tests using Selenium"
                // sh 'mvn test'
                // sh 'selenium-integration-test.sh'
            }
            post {
                always {
                    emailext to: "${env.RECIPIENT_EMAIL}",
                        subject: "Test Stage Completed - Status: ${currentBuild.result}",
                        body: "Unit and Integration tests have been completed. Please find the logs attached.",
                        attachmentsPattern: '**/build.log'
                }
            }
        }
        stage('Code Analysis') {
            steps {
                echo "Analyzing code quality using SonarQube"
                // sh 'sonar-scanner'
            }
        }
        stage('Security Scan') {
            steps {
                echo "Scanning for security vulnerabilities using OWASP Dependency-Check"
                // sh 'dependency-check.sh'
            }
            post {
                always {
                    emailext to: "${env.RECIPIENT_EMAIL}",
                        subject: "Security Scan Completed - Status: ${currentBuild.result}",
                        body: "Security scan has been completed. Please find the logs attached.",
                        attachmentsPattern: '**/build.log'
                }
            }
        }
        stage('Deploy to Staging') {
            steps {
                echo "Deploying the application to the staging environment using Ansible"
                // sh 'ansible-playbook -i staging deploy.yml'
            }
        }
        stage('Integration Tests on Staging') {
            steps {
                echo "Running integration tests in the staging environment using Selenium"
                // sh 'selenium-staging-integration-test.sh'
            }
            post {
                always {
                    emailext to: "${env.RECIPIENT_EMAIL}",
                        subject: "Integration Test Stage Completed - Status: ${currentBuild.result}",
                        body: "Integration Tests on Staging have been completed. Please find the logs attached.",
                        attachmentsPattern: '**/build.log'
                }
            }
        }
        stage('Deploy to Production') {
            steps {
                echo "Deploying the code to the production environment using Ansible"
                // sh 'ansible-playbook -i production deploy.yml'
            }
        }
    }
    post {
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed!'
        }
    }
}
