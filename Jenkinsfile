pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/본인계정/jenkins-docker-test.git'
            }
        }
        stage('Docker Build') {
            steps {
                sh 'docker build -t my-flask-app:latest .'
            }
        }
        stage('Cleanup Old Container') {
            steps {
                sh '''
                docker stop my-flask-container || true
                docker rm my-flask-container || true
                '''
            }
        }
        stage('Run Container') {
            steps {
                sh 'docker run -d --name my-flask-container -p 5001:5000 my-flask-app:latest'
            }
        }
        stage('Health Check') {
            steps {
                sh '''
                sleep 3
                curl -f http://localhost:5001 || exit 1
                '''
            }
        }
        stage('Logs') {
            steps {
                sh 'docker logs my-flask-container'
            }
        }
    }
}

