pipeline {
    agent any
    stages {
        stage('Lint HTML & Dockerfile'){
            steps {
                sh 'tidy -q -e blue-green/blue/*.html'
                sh 'tidy -q -e blue-green/green/*.html'
                sh 'hadolint blue-green/blue/Dockerfile'
                sh 'hadolint blue-green/green/Dockerfile'
            }
        }
        stage('Build and Publish Docker Image'){
                    steps {
                        sh 'docker build -t nomanikram/blueimage -f blue-green/blue/Dockerfile blue-green/blue'
                        sh 'docker build -t nomanikram/greenimage -f blue-green/green/Dockerfile blue-green/green'
                        sh 'docker push nomanikram/blueimage'
                        sh 'docker push nomanikram/greenimage'
                        sh 'docker rmi -f nomanikram/greenimage'
                        sh 'docker rmi -f nomanikram/blueimage'
                    }
                }
    }
}