pipeline {
    agent any

    environment {
        DOCKER_IMAGE = "varshithaj/app-image"
        TAG = "v1"
    }

    stages {
        stage('Clone Code') {
            steps {
                // Fixed: Removed the double 'git' keyword
                git branch: 'main', url: 'https://github.com/VarshithaJ13/docker-jenkins.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                // Fixed: Changed 'sh' to 'bat' and used Windows variable syntax
                bat "docker build -t %DOCKER_IMAGE%:%TAG% ."
            }
        }

        stage('Login to Docker Hub') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-creds',
                usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
                    // Fixed: Changed 'sh' to 'bat'
                    bat "echo %PASSWORD%| docker login -u %USERNAME% --password-stdin"
                }
            }
        }

        stage('Push Image') {
            steps {
                // Fixed: Changed 'sh' to 'bat'
                bat "docker push %DOCKER_IMAGE%:%TAG%"
            }
        }
    }
}
