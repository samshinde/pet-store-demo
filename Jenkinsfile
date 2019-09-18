#!/usr/bin/env groovy

pipeline {

  agent any

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
         sh 'mvn clean verify-P sonar -Dsonar.host.url=https://sonarcloud.io -Dsonar.organization=amol-example -Dsonar.login=684fc165294d8982b9a4837e9c2d24ef00b41e88'
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
