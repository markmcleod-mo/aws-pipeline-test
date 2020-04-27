pipeline {
  agent any
  environment {
    CI = 'true'
    HOME = '.'
    REGION = 'eu-west-2'
    CREDS = 'test-master'
  }
  options {
    withAWS(region:"${env.REGION}",credentials:"${env.CREDS}")
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
