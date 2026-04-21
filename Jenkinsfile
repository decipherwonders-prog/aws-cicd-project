pipeline {
    agent any

    stages {

        stage('Verify Workspace') {
            steps {
                sh 'pwd'
                sh 'ls -la'
                sh 'echo "Searching for server.js..."'
                sh 'find . -name server.js'
            }
        }

        stage('Build Image') {
            steps {
                sh 'docker build -t my-app:latest .'
            }
        }

        stage('Test Container Run') {
            steps {
                sh 'docker run --rm my-app:latest node server.js'
            }
        }

    }
}
