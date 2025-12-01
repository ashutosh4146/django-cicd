pipeline {
    agent any

    environment {
        IMAGE_NAME = "djangoapp"
        CONTAINER_NAME = "djangoapp"
        PORT = "8000"
    }

    stages {

        stage('Checkout Code') {
            steps {
                checkout scm
            }
        }

        stage('Build Docker Image') {
            steps {
                sh """
                    echo 'Building Docker image...'
                    docker build -t djangoapp:1.0.0 .
                """
            }
        }

        stage('Stop Old Container') {
            steps {
                sh """
                    echo 'Stopping old container if exists...'
                    docker rm -f djangoapp || true
                """
            }
        }

        stage('Run New Container') {
            steps {
                sh """
                    echo 'Starting new container...'
                    docker run -d --name hello -p 8000:8000 djangoapp:1.0.0
                """
            }
        }

    }

    post {
        success {
            echo "🚀 Deployment Completed Successfully: djangoapp:1.0.0"
        }
        failure {
            echo "❌ Deployment Failed!"
        }
    }
}
