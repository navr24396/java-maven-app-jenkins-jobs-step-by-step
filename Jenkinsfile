pipeline {
    
    agent any
    tools {
        maven 'maven3.9.12'
    }
    stages {
        stage("build jar") {
            steps {
                script {
                    echo "building the application.."
                    sh 'mvn clean package'
                }
            }
        }
        stage("build image") {
            steps {
                script {
                    echo "Build the docker image.."
                    withCredentials([usernamePassword(credentialsId: 'dockerhub', usernameVariable: 'USER', passwordVariable: 'PASS')]) {
                        sh 'docker image build -t ashok4584/java-maven-app:2.1 .'
                        sh "echo $PASS | docker login -u $USER --passsword-stdin"
                        sh 'docker image push ashok4584/java-maven-app:2.1'
                    }
                }
            }
        }
        stage("deploy") {
            script {
                echo "Deploying the application.."
            }
        }
    }