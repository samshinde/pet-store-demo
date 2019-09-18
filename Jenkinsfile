#!/usr/bin/env groovy

pipeline {

  agent { 
     docker { image 'ubuntu:18.04' }
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
