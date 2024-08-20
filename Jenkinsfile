pipeline {
    agent any

    environment {
        DOCKERHUB_CREDENTIALS = credentials('id-1') // Replace 'id-1' with your actual credentials ID
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
                    sh "docker build -t akshaykomath1/test-webapp:${imageTag} ."  // Note the change here to test-webapp
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                script {
                    def imageTag = params.IMAGE_TAG
                    echo "Pushing Docker image with tag: ${imageTag}"

                    // Authenticate and push Docker image
                    docker.withRegistry('https://index.docker.io/v1/', 'DOCKERHUB_CREDENTIALS') {
                        sh "docker push akshaykomath1/test-webapp:${imageTag}"  // Note the change here to test-webapp
                    }
                }
            }
        }
    }
}
