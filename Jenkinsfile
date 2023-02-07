pipeline{
    agent any
    stages{
        stage('Hello'){
            steps{
                echo "Hello Pipeline"   
            }
        }
    }
    post{
        always{
            echo "Always"
            slackSend(channel: "#job-notification", message: "Spring Boot Pipeline done.")
        }
        success{
            echo "Success"
        }
        failure{
            echo "Failure"
        }
        cleanup{
            echo "Cleanup"
        }
    }
}