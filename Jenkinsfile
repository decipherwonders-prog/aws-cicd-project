pipeline {
    agent any

    environment {
        IMAGE_NAME = "my-app:${BUILD_NUMBER}"
        CONTAINER_NAME = "my-app"
    }

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build Image') {
            steps {
                sh "docker build -t ${IMAGE_NAME} ."
            }
        }

        stage('Test') {
            steps {
                sh 'echo "Run tests here"'
            }
        }

        stage('Deploy') {
            steps {
                sh """
                docker stop ${CONTAINER_NAME} || true
                docker rm ${CONTAINER_NAME} || true
                docker run -d -p 80:3000 --name ${CONTAINER_NAME} ${IMAGE_NAME}
                """
            }
        }
    }

    post {
        success {
            echo "Deployment successful: ${IMAGE_NAME}"
        }
        failure {
            echo "Deployment failed. Check logs."
        }
    }
}
