pipeline {
    agent any
    tools {
        nodejs 'NodeJS'
    }
    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/Dhiraj-Kumar/NodeJS-Jenkins-CI-Demo.git', branch: 'master'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Running Test Cases') {
            steps {
                sh 'npm run test'
            }
        }

        stage('Install Docker') {
            steps {
                sh """
                    if ! command -v docker > /dev/null; then
                      sudo apt update
                      sudo apt install -y docker.io
                      sudo usermod -aG docker $(whoami)
                    fi
                """
            }
        }

        stage('Build & Deploy Docker Image') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'docker-hub-creds', usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD')]){
                    sh """
                    echo Building Docker Image
                    docker build . -t dhiraj2001/node-jenkins-app
                    
                    echo Logging into docker hub
                    docker login -u %DOCKER_USERNAME% -p %DOCKER_PASSWORD%

                    echo Pushing image to docker hub
                    docker push dhiraj2001/node-jenkins-app

                    echo Logout from docker hub
                    docker logout
                    """
                }
                 
            }
        }
    }
}