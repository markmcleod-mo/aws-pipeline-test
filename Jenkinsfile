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
        validateTemplates()
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
