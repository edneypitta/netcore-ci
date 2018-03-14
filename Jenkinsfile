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
        sh 'docker build netcore-ci-tests/'
      }
    }
    stage('Publish') {
      steps {
        step([$class: 'MSTestPublisher', testResultsFile:"**/*.trx", failOnError: true, keepLongStdio: true])
      }
    }
  }
}
