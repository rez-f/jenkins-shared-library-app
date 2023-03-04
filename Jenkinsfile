@Library('jenkins-shared-library-labs@main') _

import rez.jenkins.Output;

pipeline {
    agent any
    stages {
        stage('groovy src') {
            steps {
                script {
                    Output.hello("Groovy")
                }
            }
        }
        stage('groovy vars') {
            steps {
                script {
                    hello.world()
                }
            }
        }
    }
}