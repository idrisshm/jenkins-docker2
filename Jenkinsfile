pipeline {
  agent any

  options {
    buildDiscarder(logRotator(numToKeepStr: '5'))
  }

  environment {
    DOCKERHUB_CREDENTIALS = credentials('idrisshm')
  }

  stages {
    stage('Build') {
      steps {
        sh 'docker build -t idriss/jenkins-docker-hub2 .'
      }
    }

    stage('Login') {
      steps {
        sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
      }
    }

    stage('Push') {
      steps {
        sh 'docker push idriss/jenkins-docker-hub2'
      }
    }
  }

  post {
    always {
      sh 'docker logout'
    }
  }
}
