#!/usr/bin/env groovy

pipeline {

  agent any

  options {
    timestamps()
  }

  stages {
    stage('Sonarcloud code analysis') {
      agent {
        docker { 
          image 'maven:3-alpine' 
        }
      }
      steps {
        echo 'Checking maven version'
        sh 'mvn clean install'
        sh 'mvn sonar:sonar -Dsonar.projectKey=pet-store -Dsonar.host.url=http://localhost:9000 -Dsonar.login=decd11e66c1e4c7517cfc66673a7838dcc7a4df3'
      }
    }
    stage('Run unit tests using Junit') {
      steps {
        echo 'Running unit tests'
      }
    }
    stage('Build docker images using docker coompose inside.') {
      steps {
        echo 'Running build'
        sh './bin/build'
      }
    }
    stage('Up the built docker images and run integration tests.') {
      steps {
        echo 'Running integration tests'
        sh './test/test postgres'
        sh './test/test mysql'
      }
    }
  }

  post {
    success {
      // notify users when the Pipeline fails
      mail to: 'amol.shinde@aciworldwide.com',
          subject: "Success Pipeline: ${currentBuild.fullDisplayName}",
          body: "All things went well ${env.BUILD_URL}"
    }
    failure {
      // notify users when the Pipeline fails
      mail to: 'amol.shinde@aciworldwide.com',
          subject: "Failed Pipeline: ${currentBuild.fullDisplayName}",
          body: "Something is wrong with ${env.BUILD_URL}"
    }
  }

}
