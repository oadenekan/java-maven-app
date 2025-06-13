def gv

pipeline {
    agent any
    stages {
        stage("test") {
            steps {
                script {
                    echo "testing the application..."
                }
            }
        }
        stage("build") {
            steps {
                script {
                    echo "building the application..."
                }
            }
        }
        stage("deploy") {
            steps {
                script{
                    echo "deploying the application..."
                }
            }
        }
    }
}
