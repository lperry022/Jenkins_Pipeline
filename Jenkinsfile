pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                script {
                    echo 'Stage 1: Build - Compiling and packaging the code using Maven'
                }
                // The actual Maven command to compile and package the code
                sh 'mvn clean package'
            }
        }
        // Additional stages will be added here
    }
}
