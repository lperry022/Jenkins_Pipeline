pipeline{
    agent any
    stages{
        stage("Build"){
            steps{
                echo "Building..."
            }
        post{
            success{
                mail to: "lianaperry022@gmail.com",
                subject: "Build Status",
                body: "Build was successful!"
                }
            }
        }
    }
}
