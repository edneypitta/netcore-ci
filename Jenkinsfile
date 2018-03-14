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
      steps {
        sh 'docker login --username=_ --password=7ec33de4-e00b-4e8d-8dab-027174e1fc87 registry.heroku.com'
        sh 'docker push registry.heroku.com/netcore-ci/web'
      }
    }
  }
}