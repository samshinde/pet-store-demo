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
        mvn sonar:sonar \
 -Dsonar.projectKey=pet-store \
 -Dsonar.organization=amol-example \
 -Dsonar.host.url=https://sonarcloud.io \
 -Dsonar.login=684fc165294d8982b9a4837e9c2d24ef00b41e88
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
