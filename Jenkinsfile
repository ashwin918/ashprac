pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main',
                url: 'https://github.com/ashwin918/ashprac.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                bat '''
                set DOCKER_BUILDKIT=0
                docker build -t ashprac .
                '''
            }
        }

        stage('Run Container') {
            steps {
                bat '''
                docker stop ashprac-container
                docker rm ashprac-container
                docker run -d -p 8099:80 --name ashprac-container ashprac
                '''
            }
        }

        stage('Deploy To EC2') {
            steps {
                bat '''
                ssh -o StrictHostKeyChecking=no -i C:\\jenkins-key\\ashprac-key.pem ubuntu@3.27.160.212 "echo Connected from Jenkins"
                '''
            }
        }
    }
}
