pipeline {
    agent any
    
    environment {
        DOCKER_HUB_REGISTRY = 'fadedstarboy'
        IMAGE_NAME = 'fadedstarboy/node-app'
        TAG = 'latest'
    }
    
    stages {
        stage('Checkout') {
            steps {
                git branch: 'master', url: 'https://github.com/fadedstarboy/devops-node-rest-api.git'
            }
        }
        
        stage('Build Docker Image') {
            steps {
                script {
                    docker.build("${DOCKER_HUB_REGISTRY}/${IMAGE_NAME}:${TAG}", "-f Dockerfile .")
                }
            }
        }
        
        stage('Push Docker Image') {
            steps {
                script {
                    withCredentials([usernamePassword(credentialsId: 'DOCKER_CREDS', usernameVariable: 'Username', passwordVariable: 'Password')]) {
                        docker.withRegistry('https://index.docker.io/v1/', Username, Password) {
                            docker.image("${DOCKER_HUB_REGISTRY}/${IMAGE_NAME}:${TAG}").push()
                        }
                    }
                }
            }
        }
    }
}

