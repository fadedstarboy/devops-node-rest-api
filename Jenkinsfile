pipeline {
    agent any
    
    environment {
        DOCKER_HUB_REGISTRY = 'fadedstarboy'
        IMAGE_NAME = 'node-app'
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
                    sh 'echo $REGISTRY_CREDENTIALS_PSW | docker login -u $REGISTRY_CREDENTIALS_USR --password-stdin'
                    sh 'docker push ${DOCKER_HUB_REGISTRY}/${IMAGE_NAME}:${TAG}'
                }
            }
        }
	
        
    }
}

