pipeline {

  environment {
    CI = 'true'
    HOME = '.'
  }
  stages {
    stage('Initialise') {
      steps {
        withAWS(region:'eu-west-2',credentials:'aws-met-office-test-master') {
                accountid = sh(script: 'aws sts get-caller-identity', returnStdout: true).trim()
                echo accountid 
        }
      }
    }
    stage('Test and Build') {
      parallel {
        stage('Run Tests') {
          steps {
            withAWS(region:'eu-west-2',credentials:'aws-met-office-test-master') {
                    accountid = sh(script: 'aws sts get-caller-identity', returnStdout: true).trim()
                    echo accountid 
            }
          }
        }
        stage('Deploy Artifacts') {
          steps {
            withAWS(region:'eu-west-2',credentials:'aws-met-office-test-master') {
                    accountid = sh(script: 'aws sts get-caller-identity', returnStdout: true).trim()
                    echo accountid 
            }
          }
        }
      }
    }
    stage('Deployment Staging And Prod Parallel') {
      parallel {
        stage('Staging') {
          when {
            branch 'staging'
          }
          steps {
            echo "Only when master branch - production release only"
          }
        }
        stage('Production') {
          when {
            branch 'master'
          }
          steps {
              echo "Only when master branch - production release only"
          }
        }
      }
    }
  }
}