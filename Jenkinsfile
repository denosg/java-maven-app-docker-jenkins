pipeline {
    agent any

    tools {
        maven 'maven-3.9'
    }

    environment {
        IMAGE_NAME = "denoscos/demo-app-devops:jma-2.0"
    }

    stages {

        stage('Build JAR') {
            steps {
                echo 'Building application...'
                sh 'mvn package'
            }
        }

        stage('Build Docker Image') {
            steps {
                echo 'Building Docker image...'

                withCredentials([usernamePassword(credentialsId: 'docker-hub-repo', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
                    sh "docker build -t ${IMAGE_NAME} ."
                    sh "echo $PASSWORD | docker login -u $USERNAME --password-stdin"
                    sh "docker push ${IMAGE_NAME}"
                }
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploy stage is empty for now'
            }
        }

        stage('Cleanup') {
            steps {
                echo 'Cleanup...'
            }
        }
    }
}
