
pipeline {
    agent any

    environment {
        DOCKER_USER = 'anitamahi'
        IMAGE_NAME = 'devops-imgae.v1'
        IMAGE_TAG = 'v2'
    }

    stages {
        stage('Checkout') {
            steps {
                echo 'Downloading code from GitHub'
                checkout scm
            }
        }

        stage('Build Docker Image') {
            steps {
                echo 'Building Docker image'
                sh 'docker build -t $IMAGE_NAME:$IMAGE_TAG .'
            }
        }

        stage('Push to Docker Hub') {
            steps {
                echo 'Pushing Docker image to Docker Hub'

                withCredentials([
                    usernamePassword(
                        credentialsId: 'dockerhub-creds',
                        usernameVariable: 'DOCKER_USERNAME',
                        passwordVariable: 'DOCKER_TOKEN'
                    )
                ]) {
                    sh '''
                        set +x
                        echo "$DOCKER_TOKEN" | docker login \
                          -u "$DOCKER_USERNAME" --password-stdin

                        docker tag "$IMAGE_NAME:$IMAGE_TAG" \
                          "$DOCKER_USER/$IMAGE_NAME:$IMAGE_TAG"

                        docker push "$DOCKER_USER/$IMAGE_NAME:$IMAGE_TAG"
                        docker logout
                    '''
                }
            }
        }
    }
}
