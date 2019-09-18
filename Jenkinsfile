#!/usr/bin/env groovy

pipeline {

  agent { 
    label 'docker-slaves'
  }

  options {
    timestamps()
    buildDiscarder(logRotator(numToKeepStr: '30'))
  }

  stages {
    stage('Build Docker image') {
      steps {
        sh './bin/build'
      }
    }
  }

  post {
    always {
      cleanupAndNotify(currentBuild.currentResult)
    }
  }
}
