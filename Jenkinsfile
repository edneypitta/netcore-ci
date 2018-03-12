pipeline {
  agent any
  stages {
    stage('Install docker-compose') {
      steps {
        sh 'curl -L https://github.com/docker/compose/releases/download/1.19.0/docker-compose-`uname -s`-`uname -m` -o /usr/local/bin/docker-compose'
      }
    }
    stage('Pull & Build') {
      steps {
        sh 'docker-compose build --pull'
      }
    }
  }
}