pipeline {
  agent any
  environment {
    CI = 'true'
    HOME = '.'
  }
  stages {
    stage('Install Packages') {
      steps {
        withAWS(region:'eu-west-2',credentials:'test-master') {
          script {
            accounts = sh (script: 'aws organizations list-accounts --output text', returnStdout: true).split()
            echo accounts
          }
        }
      }
    }
    stage('Test and Build') {
      parallel {
        stage('Run Tests') {
          steps {
            sh 'java -version'
          }
        }
        stage('Create Build Artifacts') {
          steps {
            sh 'ls -al'
          }
        }
      }
    }
  }
}
