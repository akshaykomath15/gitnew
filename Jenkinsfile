pipeline {
    agent any
    environment {
        DOCKERHUB_CREDENTIALS = credentials('DOCKERHUB_CREDENTIALS')
    }
    parameters {
        string(name: 'IMAGE_TAG', defaultValue: 'latest', description: 'Tag for the Docker image')
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
                    // Use the IMAGE_TAG parameter to tag the Docker image
                    def imageTag = params.IMAGE_TAG
                    sh "docker build -t akshaykomath/node-webapp1:${imageTag} ."
                }
            }
        }
        stage('Push Docker Image') {
            steps {
                script {
                    def imageTag = params.IMAGE_TAG
                    // Authenticate with Docker Hub
                    docker.withRegistry('https://registry.hub.docker.com', 'DOCKERHUB_CREDENTIALS') {
                        // Use the Docker command to push the image with the specified tag
                        sh "docker push akshaykomath/node-webapp1:${imageTag}"
                    }
                }
            }
        }
    }
}
