@Library('jenkins-shared-library-labs@main') _

import rez.jenkins.Output;

pipeline {
    agent any
    stages {
        stage('groovy src') {
            steps {
                script {
                    Output.hello(this,"Groovy")
                }
            }
        }
        stage('groovy vars') {
            steps {
                script {
                    echo(hello())
                }
            }
        }
        stage('verbose') {
            steps {
                script {
                    def config = libraryResource("build/config.json")
                    echo(config)
                }
            }
        }
        stage('maven compile') {
            steps {
                script {
                    maven("clean")
                }
            }
        }
    }
}