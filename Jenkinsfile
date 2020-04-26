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
         //withAWS(profile:'test-master') {
          script {
            accounts = sh (script: 'aws sts assume-role --role-arn arn:aws:iam::005402609678:role/cloud-team-admin --role-session-name cloud-team-admin --output text', returnStdout: true)
            env.AWS_ACCESS_KEY_ID = accounts[5]
            env.AWS_SECRET_ACCESS_KEY = accounts[7]
            env.AWS_SESSION_TOKEN = accounts[8]
            echo "${accounts}"
            sh "aws organizations list-accounts --output text"
          }
        }
      }
    }
    stage('Test and Build') {
      parallel {
        stage('Run Tests') {
          steps {
            sh 'which aws'
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
