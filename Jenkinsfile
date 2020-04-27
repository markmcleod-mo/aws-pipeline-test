pipeline {
  agent any
  environment {
    CI = 'true'
    HOME = '.'
    REGION = 'eu-west-2'
    CREDS = 'test-master'
  }
  stages {
    stage('Assume Master Account') {
      steps {
        listOrgAccounts()
        awsIdentity()
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
                echo "suppose to list accounts"
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
