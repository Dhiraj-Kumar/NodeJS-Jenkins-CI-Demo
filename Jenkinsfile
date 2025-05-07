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

        stage('Build & Deploy Docker Image') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'docker-hub-creds', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                    sh """
                    echo Building Docker image...
                    docker build -t dhiraj2001/myapp .

                    echo Logging into Docker Hub...
                    docker login -u %DOCKER_USER% -p %DOCKER_PASS%

                    echo Pushing Docker image...
                    docker push dhiraj2001/myapp

                    echo Logging out...
                    docker logout
                    """
                }
            }
        }
    }
}
