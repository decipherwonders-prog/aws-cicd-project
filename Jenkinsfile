pipeline {
    agent any

    environment {
        AWS_REGION = "us-east-1"
        ACCOUNT_ID = "596953736819"
        IMAGE_NAME = "my-app"
        IMAGE_TAG = "${BUILD_NUMBER}"
        ECR_REPO = "596953736819.dkr.ecr.us-east-1.amazonaws.com/my-app"
        ECR_REGISTRY = "596953736819.dkr.ecr.us-east-1.amazonaws.com"
    }

    stages {

        stage('Verify Workspace') {
            steps {
                sh 'pwd'
                sh 'ls -la'
                sh 'find . -name server.js'
                sh 'test -f server.js || (echo "server.js NOT FOUND in root" && exit 1)'
            }
        }

        stage('Build Image') {
            steps {
                sh "docker build -t my-app:${IMAGE_TAG} ."
            }
        }

        stage('Tag Image') {
            steps {
                sh "docker tag my-app:${IMAGE_TAG} 596953736819.dkr.ecr.us-east-1.amazonaws.com/my-app:${IMAGE_TAG}"
            }
        }

        stage('Login to ECR') {
            steps {
                sh """
                aws ecr get-login-password --region us-east-1 | \
                docker login --username AWS --password-stdin ${ECR_REGISTRY}
                """
            }
        }

        stage('Push Image') {
            steps {
                sh "docker push 596953736819.dkr.ecr.us-east-1.amazonaws.com/my-app:${IMAGE_TAG}"
            }
        }
    }

    post {
        success {
            echo "Image pushed: ${IMAGE_TAG}"
        }
        failure {
            echo "Push failed. Check logs."
        }
    }
}
