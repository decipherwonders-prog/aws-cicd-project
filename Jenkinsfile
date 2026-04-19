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

        stage('Build Image') {
            steps {
                sh "docker build -t my-app:${IMAGE_TAG} ."
            }
        }

        stage('Tag Image') {
            steps {
                sh "docker tag my-app:20 596953736819.dkr.ecr.us-east-1.amazonaws.com/my-app:20"
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
                sh "docker push my-app:${IMAGE_TAG}"
            }
        }
    }

    post {
        success {
            echo "Image pushed: my-app:${IMAGE_TAG}"
        }
        failure {
            echo "Push failed. Check logs."
        }
    }
}
