pipeline {
  agent any

  stages {
    stage('Clone Repository') {
      steps {
        git 'https://github.com/Anjan854/ci-cd-demo.git'
      }
    }

    stage('Build Docker Image') {
      steps {
        sh 'docker build -t ci-cd-demo .'
      }
    }

    stage('Stop Existing Container') {
      steps {
        sh '''
          docker stop demo || true
          docker rm demo || true
        '''
      }
    }

    stage('Run Updated Container') {
      steps {
        sh 'docker run -d -p 3000:3000 --name demo ci-cd-demo'
      }
    }
  }

  post {
    success {
      echo '✅ Deployment Successful!'
    }
    failure {
      echo '❌ Build or Deploy Failed!'
    }
  }
}

