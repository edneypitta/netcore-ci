pipeline {
  agent any
  stages {
    stage('Pull & Build') {
      steps {
        sh 'docker-compose build --pull'
      }
    }
  }
}