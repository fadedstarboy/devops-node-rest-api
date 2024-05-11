pipeline {
    agent any
    
    environment {
        DOCKER_HUB_REGISTRY = 'fadedstarboy'
        IMAGE_NAME = 'fadedstarboy/node-app'
        TAG = 'latest'
	REGISTRY_CREDENTIALS = credentials('DOCKER_CREDS')
    }
    
    stages {
        stage('Build Docker Image') {
            steps {
                script {
                    docker.build("${DOCKER_HUB_REGISTRY}/${IMAGE_NAME}:${TAG}", "-f Dockerfile .")
                }
            }
        }
	
	stage('Push to DockerHub'){
            steps{
                script{
                    sh 'echo $REGISTRY_CREDENTIALS | docker login -u $DOCKER_HUB_REGISTRY --password-stdin'
                    sh 'docker push ${DOCKER_HUB_REGISTRY}/${IMAGE_NAME}:${TAG}'
                }
            }
        }
	
        
    }
}

