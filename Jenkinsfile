pipeline {
    agent any
    environment {
        DIRECTORY_PATH = '/var/jenkins_home' 
        TESTING_ENVIRONMENT = '6.1_Pipeline'
        PRODUCTION_ENVIRONMENT = 'Liana Perry'
        RECIPIENT_EMAIL = 'lianaperry022@gmail.com' 
    }
    stages {
        stage('Build') {
            steps {
                echo "Fetching the source code from the directory path specified by the environment variable: ${env.DIRECTORY_PATH}"
                echo "Compiling the code and generating any necessary artifacts using Maven"
                // Maven is a build automation tool used for Java projects. It manages project dependencies, compiles the source code, and packages the application (e.g., into a JAR or WAR file).
                // sh 'mvn clean package' // This command cleans the workspace (removes previous builds) and packages the project (e.g., into a JAR file).
            }
        }
        stage('Unit and Integration Tests') {
            steps {
                echo "Running unit tests using JUnit"
                echo "Running integration tests using Selenium"
                // JUnit is a testing framework for Java applications, focusing on unit testing individual components of the code.
                // Selenium is a popular tool for automating web applications for testing purposes, particularly for running integration tests where different components of the system interact.
                // sh 'mvn test' // Executes the unit tests using JUnit.
                // sh 'selenium-integration-test.sh' // A shell script to run Selenium-based integration tests.
            }
            post {
                always {
                    emailext to: "${env.RECIPIENT_EMAIL}",
                        subject: "Test Stage Completed - Status: ${currentBuild.result}",
                        body: "Unit and Integration tests have been completed. Please find the logs attached.",
                        attachLog: true
                }
            }
        }
        stage('Code Analysis') {
            steps {
                echo "Analyzing code quality using SonarQube"
                // SonarQube is a tool for continuous inspection of code quality. It provides detailed reports on code duplication, coding standards, security vulnerabilities, and more.
                // sh 'sonar-scanner' // This command runs SonarQube's analysis on the project, generating a report on code quality.
            }
        }
        stage('Security Scan') {
            steps {
                echo "Scanning for security vulnerabilities using OWASP Dependency-Check"
                // OWASP Dependency-Check is a tool that identifies project dependencies with known vulnerabilities. It checks against databases of reported vulnerabilities to ensure the application is secure.
                // sh 'dependency-check.sh' // Executes a security scan to identify any vulnerable dependencies within the project.
            }
            post {
                always {
                    emailext to: "${env.RECIPIENT_EMAIL}",
                        subject: "Security Scan Completed - Status: ${currentBuild.result}",
                        body: "Security scan has been completed. Please find the logs attached.",
                        attachLog: true
                }
            }
        }
        stage('Deploy to Staging') {
            steps {
                echo "Deploying the application to the staging environment using Ansible"
                // Ansible is an automation tool for configuration management, application deployment, and task automation. It's used here to deploy the application to the staging environment.
                // sh 'ansible-playbook -i staging deploy.yml' // Runs an Ansible playbook that contains the instructions for deploying the application to the staging environment.
            }
        }
        stage('Integration Tests on Staging') {
            steps {
                echo "Running integration tests in the staging environment using Selenium"
                // Selenium is reused in this stage to perform integration tests in the staging environment, ensuring that the application behaves as expected before moving to production.
                // sh 'selenium-staging-integration-test.sh' // A shell script to run Selenium-based integration tests on the staging environment.
            }
            post {
                always {
                    emailext to: "${env.RECIPIENT_EMAIL}",
                        subject: "Integration Test Stage Completed - Status: ${currentBuild.result}",
                        body: "Integration Tests on Staging have been completed. Please find the logs attached.",
                        attachLog: true
                }
            }
        }
    }
    post {
        success {
            echo 'Pipeline is completed successfully!'
        }
        failure {
            echo 'Pipeline failed!'
        }
    }
}
