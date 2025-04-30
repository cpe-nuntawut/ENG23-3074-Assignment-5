pipeline {
  agent any

  environment {
    IMAGE_NAME = 'assignment5-image'
    CONTAINER_NAME = 'assignment5-container'
    APP_PORT = '5000'
  }

  stages {
    stage('Clone') {
      steps {
        echo 'Cloning repository...'
        checkout scm
      }
    }

    stage('Build Docker Image') {
      steps {
        script {
          echo "Building Docker image: ${IMAGE_NAME}"
          docker.build(IMAGE_NAME)
        }
      }
    }

    stage('Run App') {
      steps {
        script {
          echo "Stopping and removing existing container (if any)..."
          sh "docker rm -f ${CONTAINER_NAME} || true"

          echo "Running new container..."
          sh """
            docker run -d --name ${CONTAINER_NAME} \
              -p ${APP_PORT}:${APP_PORT} \
              ${IMAGE_NAME}
          """
        }
      }
    }
  }

  post {
    success {
      echo '🚀 App deployed successfully.'
    }
    failure {
      echo '❌ Deployment failed.'
    }
  }
}
