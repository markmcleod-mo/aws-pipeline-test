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
            //accounts = sh (script: 'aws sts assume-role --role-arn arn:aws:iam::005402609678:role/cloud-team-admin --role-session-name cloud-team-admin --output text', returnStdout: true).split()
            sh "aws"
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
