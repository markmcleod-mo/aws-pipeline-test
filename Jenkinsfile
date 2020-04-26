pipeline {
  agent any
  environment {
    CI = 'true'
    HOME = '.'
  }
  stages {
    stage('Install Packages') {
      steps {
        assumeRole()
      }
    }
    stage('Test and Build') {
      parallel {
        stage('Run Tests') {
          steps {
            sh "aws organizations list-accounts --output text"
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

def assumeRole(Account='005402609678', Region='eu-west-2', Creds='test-master', Role='cloud-team-admin') {
  withAWS(region:"${Region}",credentials:"${Creds}") {
      accounts = sh (script: "aws sts assume-role --role-arn arn:aws:iam::${Account}:role/${Role} --role-session-name cloud-team-admin --output text", returnStdout: true).split()
      echo env.AWS_ACCESS_KEY_ID = accounts[4]
      echo env.AWS_SECRET_ACCESS_KEY = accounts[6]
      echo env.AWS_SESSION_TOKEN = accounts[7]            
  }
}
