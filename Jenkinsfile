pipeline {
  agent any
  options {
    buildDiscarder(logRotator(numToKeepStr: '5'))
  }
  environment {
    DOCKERHUB_CREDENTIALS = credentials('Docke_hub_credentials')
  }
  stages {
    stage('Build') {
      steps {
        sh 'docker build -t tegisty/jenkins-docker-image .'
      }
    }
    stage('Login') {
      steps {
        sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
      }
    }
    stage('Push') {
      steps {
        sh 'docker push tegisty13/jenkins-docker-image'
      }
    }
  }
  post {
    always {
      sh 'docker logout'
    }
  }
}