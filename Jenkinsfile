pipeline {
    agent any

    environment {
        DOCKER_USERNAME = credentials('dockerhub')
        DOCKER_PASSWORD = credentials('dockerhub')
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
                sh 'echo "$DOCKER_PASSWORD" | docker login -u "$DOCKER_USERNAME" --password-stdin'
                sh 'docker push brandonj090823/docker-node-app'
                sh 'docker logout'
            }
        }
    }
}
