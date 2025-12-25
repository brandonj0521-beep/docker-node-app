pipeline {
    agent any

    environment {
        DOCKER_CREDENTIALS = credentials('dockerhub')
    }

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/brandonj0521-beep/docker-node-app.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t brandonj090823/docker-node-app .'
            }
        }

        stage('Push to Docker Hub') {
            steps {
                sh '''
                    echo "$DOCKER_CREDENTIALS_PSW" | docker login -u "$DOCKER_CREDENTIALS_USR" --password-stdin
                    docker push brandonj090823/docker-node-app
                    docker logout
                '''
            }
        }
    }
}
