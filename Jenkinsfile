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

    stage('List Account') {
      steps {
        echo listOrgAccounts()
      }
    }
    stage('Do some other stuff') {
      steps {
        sh 'ls -al'
      }
    }

  }
}
