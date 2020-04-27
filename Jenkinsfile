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
    stage('Validate Template') {
      steps {
        cfnValidate(file:'jenkins-temp.yaml')
      }
    }
    stage('Parallel Process') {
        parallel {
          stage("List All Org Account ID's") {
            steps {
              script {
                accounts = listOrgAccounts("DEV")
                echo "${accounts}"
              }
            }
          }
          stage('Display AWS Identity') {
            steps {
              awsIdentity()
            }
          }
        }
    }
  }
}
