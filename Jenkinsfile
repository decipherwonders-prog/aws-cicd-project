pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/decipherwonders-prog/aws-cicd-project'
            }
        }

        stage('Build') {
            steps {
                echo 'Building application...'
                // add real build commands here (npm install, mvn package, etc.)
            }
        }

        stage('Test') {
            steps {
                echo 'Running tests...'
            }
        }
    }

    post {
        always {
            cleanWs()
        }
    }
}
