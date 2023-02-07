pipeline{

    agent none

    environment {
        AUTHOR = "Rez"
    }

    stages{
        stage('Verbose'){
            agent {
                node {
                    label "alpha"
                }
            }

            environment {
                USER = credentials("demo-creds")
            }

            steps {
                echo("Author: ${AUTHOR}")
                echo("Using ${USER_USR} creds")
                echo("Start Job: ${env.JOB_NAME}")
                echo("Start Build: ${env.BUILD_NUMBER}")
                echo("Branch Name: ${env.BRANCH_NAME}")
            }
        }

        stage('Init'){
            agent {
                node {
                    label "alpha"
                }
            }

            steps{
                script{
                    for (int i = 1; i <= 5; i++) {
                        echo("[${i}] Preparing...")
                    }
                }
            }
        }

        stage('Build'){
            agent {
                node {
                    label "beta"
                }
            }

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