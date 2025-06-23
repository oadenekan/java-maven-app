def gv
def BRANCH_NAME = ""


pipeline {
    agent any
    stages {
        stage("Init") {
            steps {
                script {
                    // Get the current branch name from Git
                    BRANCH_NAME = sh(script: "git rev-parse --abbrev-ref HEAD", returnStdout: true).trim()
                    echo "Branch detected: ${BRANCH_NAME}"
                }
            }
        }
        stage("test") {
            steps {
                script {
                    echo "testing the application..."
                    echo "Executing pipeline for $BRANCH_NAME"
                    echo "Testing the integration"
                }
            }
        }
        stage("build") {
            when {
                expression {
                    BRANCH_NAME == 'master'
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
                    BRANCH_NAME == 'master'
                }
            }
            steps {
                script{
                    echo "deploying the application..."
                }
            }
        }
    }
}
