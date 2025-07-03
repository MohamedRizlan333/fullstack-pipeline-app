pipeline {
    agent any

    environment {
        IMAGE_NAME = 'mohamedrizlan333/fullstack-app'
        // Optionally specify DockerHub username here if you want:
        DOCKERHUB_USERNAME = 'mohamedrizlan333'
    }

    stages {
        stage('Clone Repository') {
            steps {
                // Checkout the repository
                git branch: 'main', url: 'https://github.com/MohamedRizlan333/fullstack-pipeline-app.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                // Build Docker image with the tag from IMAGE_NAME
                sh 'docker build -t $IMAGE_NAME -f Dockerfile .'
            }
        }

        stage('Push Docker Image to DockerHub') {
            steps {
                // Login to DockerHub and push image
                withCredentials([string(credentialsId: 'dockerhub-token', variable: 'DOCKER_PASS')]) {
                    sh """
                        echo $DOCKER_PASS | docker login -u $DOCKERHUB_USERNAME --password-stdin
                        docker push $IMAGE_NAME
                    """
                }
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed. Please check the logs.'
        }
    }
}
