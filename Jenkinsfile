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
    stage('Parallel Process') {
        parallel {
          stage('List Account') {
            steps {
              listOrgAccounts()
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
