pipeline {
    agent any

    environment {
        IMAGE_NAME = "react-vite-app"
        CONTAINER_NAME = "funny_williams"
        DOCKER = "/usr/local/bin/docker"
    }

    stages {

        stage('Clone Code') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/Anzal246/DON.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh '$DOCKER build -t $IMAGE_NAME .'
            }
        }

        stage('Stop Old Container') {
            steps {
                sh '''
                $DOCKER stop $CONTAINER_NAME || true
                $DOCKER rm $CONTAINER_NAME || true
                '''
            }
        }

        stage('Run Docker Container') {
            steps {
                sh '''
                $DOCKER run -d -p 5173:5173 --name $CONTAINER_NAME $IMAGE_NAME
                '''
            }
        }
    }

    post {
        success {
            echo 'React app deployed using Docker successfully 🎉'
        }
        failure {
            echo 'Deployment failed ❌'
        }
    }
}
