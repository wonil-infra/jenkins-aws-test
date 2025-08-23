pipeline {
  agent any
  stages {
    stage('Checkout') {
      steps {
        git url: 'https://github.com/wonil-infra/jenkins-aws-test.git', branch: 'main'
      }
    }
    stage('Build Docker Image') {
      steps {
        sh '''
          echo "== Docker Build =="
          docker build -t my-flask-app:latest .
        '''
      }
    }
    stage('Run Container') {
      steps {
        sh '''
          echo "== Cleanup Old Container =="
          docker stop my-flask || true
          docker rm my-flask || true

          echo "== Run New Container =="
          docker run -d --name my-flask -p 5000:5000 my-flask-app:latest
        '''
      }
    }
  }
}

