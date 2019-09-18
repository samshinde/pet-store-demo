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
      agent {
         docker { image 'maven:3-alpine' }
      }
      steps {
         echo 'Checking maven version'
         sh 'mvn --version'
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

}
