pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        sh 'docker-compose build'
      }
    }
    stage('Test') {
      agent any
      steps {
        sh 'docker build -t unit-tests netcore-ci-tests/'
        sh 'docker run --name unit-tests-${BUILD_TAG} unit-tests'
        sh 'docker cp unit-tests-${BUILD_TAG}:/app/TestResults/output.trx .'
        step([$class: 'MSTestPublisher', testResultsFile:"output.trx", failOnError: true, keepLongStdio: true])
      }
    }
    stage('Deploy') {
      environment {
        HEROKU_TOKEN = '93341d1a-818d-435d-b4d2-404084c49737'
      }
      steps {
        sh 'docker login --username=_ --password=${HEROKU_TOKEN} registry.heroku.com'
        sh 'docker push registry.heroku.com/netcore-ci/web'
      }
    }
  }
}