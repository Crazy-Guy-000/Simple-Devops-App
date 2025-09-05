pipeline {
  agent any

  stages {
    stage('Build Docker Image') {
      steps {
        script {
          def gitSha = sh(returnStdout: true, script: 'git rev-parse --short HEAD').trim()
          def imageName = "simple-devops-app:${gitSha}"

          sh "docker build -t ${imageName} ."

          env.IMAGE_NAME = imageName
        }
      }
    }

    stage('Deploy to Docker') {
      steps {
        script {
          sh "docker stop simple-app || true"
          sh "docker rm simple-app || true"

          sh "docker run -d --name simple-app -p 3000:3000 ${env.IMAGE_NAME}"
        }
      }
    }
  }
}