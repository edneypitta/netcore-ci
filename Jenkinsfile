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
        sh 'mstest testResultsFile:"**/*.trx", keepLongStdio: true'
      }
    }
  }
}