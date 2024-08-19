pipeline {
    agent any
    environment {
        DOCKERHUB_CREDENTIALS = credentials('DOCKERHUB_CREDENTIALS')
    }
    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/akshaykomath15/gitnew.git', branch: 'main'
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                    // Build the Docker image and tag it
                    sh 'docker buildx build -t akshaykomath/node-webapp1:v1 .'
                    
                    // Note: No need to store dockerImage in environment variable
                }
            }
        }
        stage('Push Docker Image') {
            steps {
                script {
                    // Authenticate with Docker Hub
                    docker.withRegistry('https://registry.hub.docker.com', 'DOCKERHUB_CREDENTIALS') {
                        // Use the Docker command to push the image directly
                        sh 'docker push akshaykomath/node-webapp1:v1'
                    }
                }
            }
        }
    }
}
