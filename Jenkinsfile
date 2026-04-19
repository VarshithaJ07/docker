pipeline {
    agent any

    environment {
        DOCKER_IMAGE = "varshithaj21/app-image"
        TAG = "v1"
    }

    stages {

        stage('Clone Code') {
            steps {
                git 'https://github.com/VarshithaJ07/docker.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $DOCKER_IMAGE:$TAG .'
            }
        }

        stage('Login to Docker Hub') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-creds',
                usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
                    sh 'echo $PASSWORD | docker login -u $USERNAME --password-stdin'
                }
            }
        }

        stage('Push Image') {
            steps {
                sh 'docker push $DOCKER_IMAGE:$TAG'
            }
        }
    }
}
    post {
        success {
            echo 'Image successfully built and pushed to Docker Hub'
        }
        failure {
            echo 'Pipeline failed'
        }
    }
}
