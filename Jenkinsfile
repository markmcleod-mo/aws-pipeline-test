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
    parallel {

        stage('List Account') {
          steps {
            script {
            accounts = sh ("aws organizations list-accounts --output text", returnStdout: true).split()
            echo "${accounts}"
            }
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
