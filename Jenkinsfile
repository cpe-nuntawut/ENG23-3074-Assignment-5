pipeline {
  agent any

  stages {
    stage('Clone') {
      steps {
        git 'https://github.com/your-username/ci-cd-demo.git'
      }
    }

    stage('Build Docker Image') {
      steps {
        script {
          docker.build('ci-cd-demo:latest')
        }
      }
    }

    stage('Run Container') {
      steps {
        script {
          sh 'docker rm -f ci-cd-app || true'
          sh 'docker run -d --name ci-cd-app -p 5000:5000 ci-cd-demo:latest'
        }
      }
    }
  }
}
