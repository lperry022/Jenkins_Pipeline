pipeline {
    agent any
    environment {
        RECIPIENT_EMAIL = 'lianaperry022@gmail.com'
    }
    stages {
        stage('Test Email') {
            steps {
                emailext to: "${env.RECIPIENT_EMAIL}",
                    subject: "Test Email - Status: ${currentBuild.result}",
                    body: "This is a test email to verify email configuration.",
                    attachmentsPattern: '**/build.log'
            }
        }
    }
}
