pipeline {

  environment {
    CI = 'true'
    HOME = '.'
  }
  stages {
    stage('Initialise') {
      withAWS(region:'eu-west-2',credentials:'aws-met-office-test-master') {
      steps {
        
                accountid = sh(script: 'aws sts get-caller-identity', returnStdout: true).trim()
                echo accountid 
        }
      }
    }
    stage('Test and Build') {
      parallel {
        stage('Run Tests') {
          withAWS(region:'eu-west-2',credentials:'aws-met-office-test-master') {
          steps {
            
                    accountid = sh(script: 'aws sts get-caller-identity', returnStdout: true).trim()
                    echo accountid 
            }
          }
        }
        stage('Deploy Artifacts') {
          withAWS(region:'eu-west-2',credentials:'aws-met-office-test-master') {
          steps {
            
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
