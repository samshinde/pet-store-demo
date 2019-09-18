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
    stage('Sonarcloud code analysis') {
      steps {
        echo 'Running code analysis'
      }
    }
    stage('Run unit tests using Junit') {
      steps {
        echo 'Running unit tests'
      }
    }
    stage('Build using maven') {
      steps {
        echo 'Running build'
      }
    }
  }

  post {
    always {
      cleanupAndNotify(currentBuild.currentResult)
    }
  }
}
