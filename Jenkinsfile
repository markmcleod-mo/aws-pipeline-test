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
        //listOrgAccounts()
        //assumeRole()
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
                echo "LIST OF ACCOUNTS" + org.getListOrgAccts()
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
