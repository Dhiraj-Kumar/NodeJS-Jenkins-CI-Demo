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
    }
}