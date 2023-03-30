pipeline {
  agent {label 'node-2'}
  options {
    buildDiscarder(logRotator(numToKeepStr: '5'))
  }
  environment {
    DOCKERHUB_CREDENTIALS = credentials('dockerhub')
  }
  stages {
    stage('Build') {
      steps {
        sh 'sudo docker build -t temirlanbaisalov/jenkins-docker-hub .'
      }
    }
    stage('Login') {
      steps {
        sh 'echo $DOCKERHUB_CREDENTIALS_PSW | sudo docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
      }
    }
    stage('Push') {
      steps {
        sh 'sudo docker push temirlanbaisalov/jenkins-docker-hub'
      }
    }
  }
  post {
    always {
      sh 'sudo docker logout'
    }
  }
}