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
                    def dockerImage = docker.build('akshaykomath/node-webapp:v1')
                    
                    // Optionally, store the image name if needed for later stages
                    env.DOCKER_IMAGE = dockerImage.imageName
                }
            }
        }
        stage('Push Docker Image') {
            steps {
                script {
                    // Authenticate with Docker Hub
                    docker.withRegistry('https://registry.hub.docker.com', 'DOCKERHUB_CREDENTIALS') {
                        // Use the previously built Docker image
                        def dockerImage = docker.image(env.DOCKER_IMAGE)
                        
                        // Push the Docker image with tags
                        dockerImage.push('latest')  // Optionally specify tags like 'latest'
                        dockerImage.push('v1')      // Push the versioned tag
                    }
                }
            }
        }
    }
}
