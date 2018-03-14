pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        sh 'docker-compose build'
      }
    }
    stage('Run tests') {
      steps {
        sh 'docker build -t unit-tests netcore-ci-tests/'
        sh 'docker run --name unit-tests unit-tests'
        sh 'docker cp unit-tests:/app/TestResults/output.trx .'
      }
    }
  }
}