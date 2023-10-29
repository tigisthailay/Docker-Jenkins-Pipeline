pipeline {
  //agent any or
  agent {
    label 'docker' 
  }
  options {
    buildDiscarder(logRotator(numToKeepStr: '5'))
  }
  environment {
    DOCKERHUB_CREDENTIALS = credentials('Docke_hub_credentials')
  }
  stages {
    stage('Build') {
      steps {
        sh 'docker build -t tegisty/data2bots-docker-image .'
      }
    }
    stage('Login') {
      steps {
        sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
      }
    }
    stage('Push') {
      steps {
        sh 'docker push tegisty13/data2bots-docker-image'
      }
    }
  }
  post {
    always {
      sh 'docker logout'
    }
  }
}