pipeline{
    agent any
    stages{
        stage('Hello'){
            steps{
                echo "Hello Pipeline"   
            }
        }
        stage('Build'){
            steps{
                sh('./mvnw clean')
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