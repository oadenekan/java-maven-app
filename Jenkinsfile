def gv

pipeline {
    agent any
    tools {
        maven "Maven"
    }
    stages {
        stage ("increment version"){
            steps {
                script {
                    echo "incrementing app version"
                    sh 'mvn build-helper:parse-version versions:set \
                        -DnewVersion=\\\${parsedVersion.majorVersion}.\\\${parsedVersion.minorVersion}.\\\${parsedVersion.nextIncrementalVersion} \
                        versions:commit'
                    def matcher = readFile('pom.xml') =~ '<version>(.+)</version>'
                    def version = matcher[0][1]
                    env.IMAGE_NAME = "$version-$BUILD_NUMBER"
               }
            }
        }
        stage("build app") {
            steps {
                script {
                    echo "building the application..."
                    sh "mvn clean package"
                }
            }
        }
        stage("build image") {
            steps {
                script {
                    echo "building the docker image..."
                    withCredentials([usernamePassword(credentialsId: "docker-hub-repo", passwordVariable: "PASS", usernameVariable: "USER")]) {
                        sh '''
                            docker build -t olusolaayeni/demo-app:${IMAGE_NAME} .
                            echo "$PASS" | docker login -u "$USER" --password-stdin
                            docker push olusolaayeni/demo-app:${IMAGE_NAME}
                        '''
                    }
                }
            }
        }
        stage("deploy") {
            steps {
                script{
                    echo "deploying docker image..."
                }
            }
        }
        stage("commit version update") {
            steps {
                script {
                    sshagent(['GitHub-ssh']) {
                        sh 'git config --global user.email "jenkins@example.com"'
                        sh 'git config --global user.name "jenkins"'
                        sh "git remote set-url origin git@github.com:oadenekan/java-maven-app.git"

                        sh '''
                            mkdir -p ~/.ssh
                            ssh-keyscan github.com >> ~/.ssh/known_hosts
                        '''

                        sh 'git add .'
                        sh 'git commit -m "ci: version bump" || echo "Nothing to commit"'
                        sh 'git push origin HEAD:Jenkins-jobs'
                    }
                }
            }
        }
    }
}
