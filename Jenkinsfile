pipeline {
    agent any
    stages {
        stage('Test Email') {
            steps {
                Post{
            mail to: "lianaperry022@gmail.com",
            subject: "Build Status"
            body: "Build was successful!"
        }
            }
        }
    }
}
