pipeline {
    agent any

    environment {
        DOCKER_IMAGE = "myapp:latest"
        REPO_URL = "https://github.com/daxdobariya/mydemo.git"
    }

    stages {

        stage('Clone Repository') {
            steps {
                git branch: 'main', url: "${REPO_URL}"
            }
        }

        stage('Build Docker Image') {
            steps {
                sh '''
                echo "Building Docker image..."
                docker build -t ${DOCKER_IMAGE} .
                '''
            }
        }

        stage('Run Docker Container') {
            steps {
                sh '''
                echo "Running container..."
                docker rm -f myapp-container
                docker run -d -p 80:80 --name myapp-container ${DOCKER_IMAGE} || true
                '''
            }
        }
    }

    post {
        always {
            sh 'docker ps -a'
        }
    }
}
