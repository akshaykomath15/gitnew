pipeline {
    agent any
    environment {
        DOCKERHUB_CREDENTIALS = credentials('cdc8f42b-2abf-4c4e-85e6-c55d6ba03d7b')
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
               sh 'docker build -t akshaykomath/node-webapp:v1
 
                }
            }
        }
        stage('Push Docker Image') {
            steps {
                script {
                    docker.withRegistry('https://registry.hub.docker.com', 'DOCKERHUB_CREDENTIALS') {
                        dockerImage.push()
                    }
                }
            }
        }
    }
}
