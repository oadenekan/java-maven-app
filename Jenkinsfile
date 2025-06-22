#!/user/bin/env groovy

library identifier: "jenkins-shared-library@master", retriever: modernSCM(
    [$class: "GitSCMSource",
    remote: "https://github.com/oadenekan/jenkins-shared-library.git",
    credentialsId: "GitHub-credentials"])

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
