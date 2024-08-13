pipeline {
    agent any
    environment {
        DIRECTORY_PATH = '/var/jenkins_home'
        TESTING_ENVIRONMENT = '6.1_Pipeline'
        PRODUCTION_ENVIRONMENT = 'Liana Perry'
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
                    mail to: "lianaperry022@gmail.com",
                        subject: "Test Stage Completed - Status: ${currentBuild.result}",
                        body: "Unit and Integration tests have been completed. Please find the logs attached.",
                        attachLog: true
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
                    mail to: "lianaperry022@gmail.com",
                        subject: "Security Scan Completed - Status: ${currentBuild.result}",
                        body: "Security scan has been completed. Please find the logs attached.",
                        attachLog: true
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
                    mail to: "lianaperry022@gmail.com",
                        subject: "Intergration Test Stage Completed - Status: ${currentBuild.result}",
                        body: "Intergration Tests on Staging have been completed. Please find the logs attached.",
                        attachLog: true
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
