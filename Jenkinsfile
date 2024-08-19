pipeline {
    agent any
   
    environment {
        DOCKERHUB_CREDENTIALS = credentials('id-1')
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
                    def imageTag = params.IMAGE_TAG
                    echo "Building Docker image with tag: ${imageTag}"
                     bat "docker build -t akshaykomath/node-webapp1:${imageTag} ."
                }
            }
        }
        stage('Push Docker Image') {
            steps {
                script {
                    def imageTag = params.IMAGE_TAG
                    echo "Pushing Docker image with tag: ${imageTag}"
                    
                    docker.withRegistry('https://registry.hub.docker.com', 'id-1') {
                        sh "docker push akshaykomath/node-webapp1:${imageTag}"
                    }
                }
            }
        }
    }
}
