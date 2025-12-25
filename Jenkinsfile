pipeline {
    agent any

    environment {
        DOCKER_IMAGE = 'brandonj090823/docker-node-app' // <--- your Docker Hub repo
        IMAGE_TAG = 'latest'
        DOCKERHUB_CREDENTIALS = credentials('dockerhub') // <--- this is what you named your Jenkins Docker credentials
    }

   stage('Checkout') {
    steps {
        git branch: 'main', url: 'https://github.com/brandonj0521-beep/docker-node-app.git'
    }
}
        }

        stage('Build Docker Image') {
            steps {
                script {
                    docker.build("${DOCKER_IMAGE}:${IMAGE_TAG}")
                }
            }
        }

        stage('Push to Docker Hub') {
            steps {
                script {
                    docker.withRegistry('https://index.docker.io/v1/', "${DOCKERHUB_CREDENTIALS}") {
                        docker.image("${DOCKER_IMAGE}:${IMAGE_TAG}").push()
                        docker.image("${DOCKER_IMAGE}:${IMAGE_TAG}").push('latest')
                    }
                }
            }
        }
    }

    post {
        success {
            echo "Docker image ${DOCKER_IMAGE}:${IMAGE_TAG} pushed successfully!"
        }
        failure {
            echo "Pipeline failed."
        }
    }
}
