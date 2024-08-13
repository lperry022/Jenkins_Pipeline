pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                script {
                    // Build the code using Maven
                    sh 'mvn clean package'
                }
            }
        }

        stage('Unit and Integration Tests') {
            steps {
                script {
                    // Run unit and integration tests using JUnit the automatiom tool
                    sh 'mvn test'
                }
            }
            post {
                always {
                    // Send email notification with logs attached
                    emailext (
                        to: 'lianaperry022@gmail.com',
                        subject: "Build: ${currentBuild.fullDisplayName} - Unit and Integration Tests",
                        body: "Unit and Integration Tests ${currentBuild.currentResult}. Please see attached logs.",
                        attachLog: true
                    )
                }
            }
        }

        stage('Code Analysis') {
            steps {
                script {
                    // Run code analysis using SonarQube to ensure code meets industry standards
                    withSonarQubeEnv('SonarQube') {
                        sh 'mvn sonar:sonar'
                    }
                }
            }
        }

        stage('Security Scan') {
            steps {
                script {
                    // Run security scan using OWASP Dependency-Check to ensure there are no vulnerabilities
                    sh 'mvn dependency-check:check'
                }
            }
            post {
                always {
                    // Send email notification with logs attached
                    emailext (
                        to: 'lianaperry022@gmail.com',
                        subject: "Build: ${currentBuild.fullDisplayName} - Security Scan",
                        body: "Security Scan ${currentBuild.currentResult}. Please see attached logs.",
                        attachLog: true
                    )
                }
            }
        }

        stage('Deploy to Staging') {
            steps {
                script {
                    // Deploy to staging using Ansible
                    sh 'ansible-playbook -i inventory/staging deploy.yml'
                }
            }
        }

        stage('Integration Tests on Staging') {
            steps {
                script {
                    // Run integration tests on staging using Selenium
                    sh 'mvn verify -Pstaging'
                }
            }
        }
        post {
                always {
                    // Send email notification with logs attached
                    emailext (
                        to: 'lianaperry022@gmail.com',
                        subject: "Build: ${currentBuild.fullDisplayName} - Intergration Test",
                        body: "Intergration test ${currentBuild.currentResult}. Please see attached logs.",
                        attachLog: true
                    )
                }
            }

        stage('Deploy to Production') {
            steps {
                script {
                    // Deploy to production using Ansible
                    sh 'ansible-playbook -i inventory/production deploy.yml'
                }
            }
        }
    }

    post {
        success {
            // Send a success notification email
            emailext (
                to: 'lianaperry022@gmail.com',
                subject: "Build Success: ${currentBuild.fullDisplayName}",
                body: "The build was successful."
            )
        }
        failure {
            // Send a failure notification email
            emailext (
                to: 'lianaperry022@gmail.com',
                subject: "Build Failed: ${currentBuild.fullDisplayName}",
                body: "The build failed. Please check the logs."
            )
        }
    }
}
