pipeline{
    agent any
    environment {
        DIRECTORY_PATH = '/var/jenkins_home'
        TESTING_ENVIRONMENT = '6.1_Pipeline'
        PRODUCTION_ENVIRONMENT = 'Liana Perry'
    }
    stages{
        stage("Build"){
            steps{
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
                        body: "Unit and Integration tests have been completed. Please find the logs attached."                }
            }
        }
    }
}
