pipeline {
  agent any
  environment {
    CI = 'true'
    HOME = '.'
  }
  stages {
    stage('Assume Master Account') {
      steps {
        assumeRole()
      }
    }
    stage('Parallel Process') {
        parallel {
          stage('List All Org Account ID''s') {
            steps {
              accounts = listOrgAccounts()
              echo "${accounts}"
            }
          }
          stage('Do some other stuff') {
            steps {
              sh 'ls -al'
            }
          }
        }
    }
  }
}
