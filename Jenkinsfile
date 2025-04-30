pipeline {
  agent any

  stages {
    stage('Clone') {
      steps {
        checkout scm
      }
    }

    stage('Build Docker Image') {
      steps {
        script {
          docker.build('assignment5-image')
        }
      }
    }

    stage('Run App') {
      steps {
        script {
          sh 'docker rm -f assignment5-container || true'
          sh 'docker run -d --name assignment5-container -p 5000:5000 assignment5-image'
        }
      }
    }
  }
}
