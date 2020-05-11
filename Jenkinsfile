pipeline {
    agent {
        label 'docker-agent'
    }
  environment {
    CI = 'true'
    HOME = '.'
    npm_config_cache = 'npm-cache'
      env.REGION = 'eu-west-2'
      env.CREDS = 'test-master'
      //Initialise what needs to be built and checkout the SCM
      checkout scm
      //Find all of the accounts in the management OU only, for now
      accounts = org.getOrgAcctsByType("005402609678", "cloud-team-admin", "DEV")
      echo "Pipeline - : ${accounts}"
  }
  stages {
    stage('Install Packages') {
      steps {
        sh 'pwd'
      }
    }
    stage('Test and Build') {
      parallel {
        stage('Run Tests') {
          steps {
            sh 'java -version'
          }
        }
        stage('Create Build Artifacts') {
          steps {
            sh 'ls -al'
          }
        }
      }
    }
    stage('Deployment') {
      parallel {
        stage('Staging') {
          when {
            branch 'staging'
          }
          steps {
            withAWS(region:'<your-bucket-region>',credentials:'<AWS-Staging-Jenkins-Credential-ID>') {
              s3Delete(bucket: '<bucket-name>', path:'**/*')
              s3Upload(bucket: '<bucket-name>', workingDir:'build', includePathPattern:'**/*');
            }
            mail(subject: 'Staging Build', body: 'New Deployment to Staging', to: 'jenkins-mailing-list@mail.com')
          }
        }
        stage('Production') {
          when {
            branch 'master1'
          }
          steps {
            withAWS(region:'<your-bucket-region>',credentials:'<AWS-Production-Jenkins-Credential-ID>') {
              s3Delete(bucket: '<bucket-name>', path:'**/*')
              s3Upload(bucket: '<bcket-name>', workingDir:'build', includePathPattern:'**/*');
            }
            mail(subject: 'Production Build', body: 'New Deployment to Production', to: 'jenkins-mailing-list@mail.com')
          }
        }
      }
    }
  }
}
