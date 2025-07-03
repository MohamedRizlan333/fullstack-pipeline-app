pipeline {
    agent any

    environment {
        IMAGE_NAME = 'mohamedrizlan333/fullstack-app'
    }

    stages {
        stage('Clone Repository') {
            steps {
                git 'https://github.com/MohamedRizlan333/fullstack-pipeline-app.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $IMAGE_NAME -f DockerBuildfile .'
            }
        }

        stage('Push Docker Image to DockerHub') {
            steps {
                withCredentials([string(credentialsId: 'dockerhub-token', variable: 'DOCKER_PASS')]) {
                    sh """
                        echo $DOCKER_PASS | docker login -u mohamedrizlan333 --password-stdin
                        docker push $IMAGE_NAME
                    """
                }
            }
        }
    }
}
