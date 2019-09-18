#!/usr/bin/env groovy

pipeline {

  agent {
    docker {
      reuseNode true 
      image 'maven:3-alpine' 
    }
  }

  options {
    timestamps()
  }

  stages {
    stage('Sonarcloud code analysis') {
      steps {
         echo 'Checking maven version'
         sh 'mvn --version'
         sh 'mvn sonar:sonar -Dsonar.projectKey=pet-store -Dsonar.host.url=https://sonarcloud.io -Dsonar.organization=amol-example -Dsonar.login=684fc165294d8982b9a4837e9c2d24ef00b41e88'
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
    failure {
      // notify users when the Pipeline fails
      mail to: 'amol.shinde@aciworldwide.com',
          subject: "Failed Pipeline: ${currentBuild.fullDisplayName}",
          body: "Something is wrong with ${env.BUILD_URL}"
    }
  }

}
