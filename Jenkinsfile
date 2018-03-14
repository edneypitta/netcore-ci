pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        sh 'docker-compose build'
      }
    }
    stage('Run tests') {
      agent any
      steps {
        sh 'docker build -t unit-tests netcore-ci-tests/'
        sh 'docker run --name unit-tests-${BUILD_TAG} unit-tests'
        sh 'docker cp unit-tests-${BUILD_TAG}:/app/TestResults/output.trx .'
        step([$class: 'MSTestPublisher', testResultsFile:"output.trx", failOnError: true, keepLongStdio: true])
      }
    }
  }
}