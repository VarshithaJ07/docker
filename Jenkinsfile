pipeline{
    agent any
    environment{
        DOCKER_IMAGE="varshithaj21/myimage"
        TAG="v1"
    }
    stages{
        stage('Clone Code'){
            steps{
                git branch:"main", url:"https://github.com/VarshithaJ07/docker.git"
            }
        }

        stage('Build Docker Image'){
            steps{
                bat "docker build -t %DOCKER_IMAGE%:%TAG% ."
            }
        }
        stage('Login to Docker Hub'){
            steps{
                withCredentials([usernamePassword(
                    credentiaslId:'dockerhub-creds',
                    usernameVariable:'USERNAME',
                    passwordVariable:'PASSWORD')]){
                        bat "echo %PASSWORD%| docker login -u %USERNAME% --password-stdin"
                    }
            }

        }
        stage('Push Image'){
            steps{
                bat "docker push %DOCKER_IMAGE%:%TAG%"
            }

        } 
        post{
            success{
                echo "docker image pushed successfully"
            }
            failure{
                echo "failed to push docker image"
            }
        }
    }
}