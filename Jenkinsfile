pipeline{

    agent none

    environment {
        AUTHOR = "Rez"
    }

    parameters {
        booleanParam(name: 'DEPLOY', defaultValue: false, description: 'Deploy after build?')
    }

    options {
        disableConcurrentBuilds()
        timeout(time: 2, unit: 'MINUTES')
    }

    triggers {
        pollSCM("*/5 * * * *")
    }

    stages{
        stage('Verbose'){
            environment {
                USER = credentials("demo-creds")
            }

            parallel {

                stage('Connecting to VM...'){
                    agent {
                        node {
                            label "alpha"
                        }
                    }

                    steps {
                        echo("Connecting... ... ... ... .")
                    }
                }
                
                stage('Print') {
                    agent {
                        node {
                            label "alpha"
                        }
                    }

                    steps {
                        echo("Author: ${AUTHOR}")
                        echo("Using ${USER_USR} creds")
                        echo("Start Job: ${env.JOB_NAME}")
                        echo("Start Build: ${env.BUILD_NUMBER}")
                        echo("Branch Name: ${env.BRANCH_NAME}")
                    }
                }

                stage('Cleaning up') {
                    agent {
                        node {
                            label "alpha"
                        }
                    }
                    
                    steps {
                        echo("Cleaning up...")
                    }
                }
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
                    echo("Deployment status ${params.DEPLOY}")

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

        stage('Deploy'){
            agent {
                node {
                    label "beta"
                }
            }

            input {
                message "Deploy now?"
                ok "Yes"
                submitter "admin"
                parameters {
                    choice(name: "ENVIRONMENT", choices: ['DEV', 'STAGING', 'PRODUCTION'], description: "Deployment Environment")
                }
            }

            steps {
                echo "Deploy step"
            }
        }

        stage('Release'){
            agent {
                node {
                    label "beta"
                }
            }

            when {
                expression {
                    return params.DEPLOY
                }
            }

            steps {
                echo "Performing release..."
            }
        }
    }

    post{
        always{
            echo "Always"
            slackSend(channel: "#job-notification", message: "[${env.BUILD_NUMBER}] Spring Boot Pipeline done.")
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