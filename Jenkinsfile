pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building the code using Maven...'
                sh 'mvn clean package'  // Runs Maven to build the project
            }
        }

        stage('Unit and Integration Tests') {
            steps {
                echo 'Running unit and integration tests...'
                sh 'mvn test'  // Runs unit and integration tests using Maven
            }
        }

        stage('Code Analysis') {
            steps {
                echo 'Analyzing the code using SonarQube...'
                // Assuming SonarQube is set up and configured in Jenkins
                withSonarQubeEnv('SonarQube') {
                    sh 'mvn sonar:sonar'  // Runs SonarQube analysis
                }
            }
        }

        stage('Security Scan') {
            steps {
                echo 'Scanning for security vulnerabilities...'
                // Assuming OWASP Dependency-Check is set up in Jenkins
                sh 'mvn org.owasp:dependency-check-maven:check'  // Runs OWASP Dependency-Check
            }
        }

        stage('Deploy to Staging') {
            steps {
                echo 'Deploying the application to the staging environment...'
                // Deploy to Staging using Ansible or AWS CLI commands
                sh 'ansible-playbook -i inventory/staging deploy.yml'
            }
        }

        stage('Integration Tests on Staging') {
            steps {
                echo 'Running integration tests on the staging environment...'
                // Runs integration tests on the staging environment
                sh 'mvn verify -Pintegration-test'
            }
        }

        stage('Deploy to Production') {
            steps {
                echo 'Deploying the application to production...'
                // Deploy to Production using Ansible or AWS CLI commands
                sh 'ansible-playbook -i inventory/production deploy.yml'
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed.'
        }
        always {
            mail to: 'lianaperry022@gmail.com',
                 subject: "Pipeline status: ${currentBuild.currentResult}",
                 body: "Pipeline ${env.JOB_NAME} build ${env.BUILD_NUMBER} completed with status: ${currentBuild.currentResult}",
                 attachLog: true
        }
    }
}
