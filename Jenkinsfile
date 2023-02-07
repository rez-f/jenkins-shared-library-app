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