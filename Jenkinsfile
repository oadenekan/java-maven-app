#!/user/bin/env groovy

@Library('jenkins-shared-library') //import the library code from jenkins custom global system
def gv

pipeline {
    agent any
    tools {
        maven 'Maven'
    }
    stages {
        stage("init") {
            steps {
                script {
                    gv = load "script.groovy"
                }
            }
        }
        stage("build jar") {
            steps {
                script {
                    buildJar()
                }
            }
        }
        stage("build and push image") {
            steps {
                script {
                    buildImage "olusolaayeni/demo-app:jma-3.0"
                    dockerLogin()
                    dockerPush "olusolaayeni/demo-app:jma-3.0"
                }
            }
        }
        stage("deploy") {
            steps {
                script{
                    gv.deployApp()
                }
            }
        }
    }
}
