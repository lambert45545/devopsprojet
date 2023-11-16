pipeline {
  agent any
  options {
    buildDiscarder(logRotator(numToKeepStr: '5'))
  }
  environment {
    DOCKERHUB_CREDENTIALS = credentials('lambertahmed-dockerhub')
  }
  stages {
    stage('Build') {
      steps {a
        sh 'docker build -t ahmed/dp-alpine:latest .'
      }
    }
    stage('Login') {
      steps {
        sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
      }
    }
    stage('Push') {
      steps {
        sh 'docker push ahmed/dp-alpine:latest'
      }
    }
  }
  post {
    always {
      sh 'docker logout'
    }
  }
}
