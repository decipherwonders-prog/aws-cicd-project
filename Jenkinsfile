pipeline {
    agent any

    stages {

        stage('Build Image') {
            steps {
                sh 'docker build -t my-app:${BUILD_NUMBER} .'
            }
        }

        stage('Test') {
            steps {
                sh 'echo "Run tests here"'
            }
        }

        stage('Deploy') {
            steps {
                sh '''
                docker stop my-app || true
                docker rm my-app || true
                docker run -d -p 80:3000 --name my-app my-app:${BUILD_NUMBER}
                '''
            }
        }
    }
}
