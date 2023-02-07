pipeline{
    agent any
    stages{
        stage('Init'){
            steps{
                script{
                    for (int i = 0; i <= 5; i++) {
                        echo("[${i}] Preparing...")
                    }
                }
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