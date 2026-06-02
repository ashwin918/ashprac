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
                docker run -d -p 8082:80 --name ashprac-container ashprac
                '''
            }
        }
    }
}
