pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        sh 'docker-compose build --pull'
      }
    }
    stage('Run tests') {
      steps {
        sh 'pwd && ls'
      }
    }
  }
}