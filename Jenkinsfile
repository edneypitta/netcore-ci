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
        sh 'docker-compose -f "netcore-ci-tests/docker-compose.yml" run unit-tests'
      }
    }
  }
}