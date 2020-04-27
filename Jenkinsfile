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
              sh "aws organizations list-accounts --output text"
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
