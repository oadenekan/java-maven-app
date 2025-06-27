def gv

pipeline {
    agent any
    stages {
        stage('Detect Branch') {
            steps {
                script {
                    env.BRANCH_NAME = sh(script: "git rev-parse --abbrev-ref HEAD", returnStdout: true).trim()
                    echo "Detected branch: ${env.BRANCH_NAME}"
                }
            }
        }
        stage("test") {
            steps {
                script {
                    echo "testing the application..."
                    echo "Executing pipeline for ${env.BRANCH_NAME}"
                    echo "testing the integration"
                }
            }
        }
        stage("build") {
            when {
                expression {
                    env.BRANCH_NAME == 'master'
                }
            }
            steps {
                script {
                    echo "building the application..."
                }
            }
        }
        stage("deploy") {
            when {
                expression {
                    env.BRANCH_NAME == 'master'
                }
            }
            steps {
                script {
                    echo "deploying the application..."
                }
            }
        }
    }
}