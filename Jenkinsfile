  def buildNumber = env.BUILD_NUMBER
  def workspace = env.WORKSPACE
  def buildUrl = env.BUILD_URL

  def builds = []
  def tasks = [:]

  /*
    Initialise stage:
  */
  stage 'Initialise'

    node {
      agent any
      env.REGION = 'eu-west-2'
      env.CREDS = 'test-master'
      //Initialise what needs to be built and checkout the SCM
      checkout scm
      //Find all of the accounts in the management OU only, for now
      //accounts = org.getOrgAcctsByType("005402609678", "cloud-team-admin", "DEV")
      //echo "Pipeline - : ${accounts}"
    }

  stage 'Validate Templates'
    for(String item: accounts) {
      def account_path = item
      tasks["${item}"] = {
        node {
          echo "account_path=${account_path}"
          checkout scm
          //validateTemplates("./", "${account_path}", "cloud-team-admin")
        }
      }
    }

    try {
      parallel tasks
    } catch (e) {
      // If there was an exception thrown, the build failed
      throw e
    } finally {
      tasks = [:]
    }

    stage 'Deploy Stack'
    //Loop through all accoun  ts found and build a paralle task for each
    for(String item: accounts) {
      def account_path = item
      tasks["${item}"] = {
        node {
          echo "account=${account_path}"
          //checkout scm
          //deployStack("Jenkins-Pipeline", "${account_path}", "cloud-team-admin")
        }
      }
    }

    try {
      parallel tasks
    } catch (e) {
      // If there was an exception thrown, the build failed
      throw e
    } finally {
      tasks = [:]
    }

    stage 'Desribe Stack'
    //Loop through all accoun  ts found and build a paralle task for each
    for(String item: accounts) {
      def account_path = item
      tasks["${item}"] = {
        node {
          echo "account=${account_path}"
          checkout scm
          //describeStack("Jenkins-Pipeline", "${account_path}", "cloud-team-admin")
        }
      }
    }

    try {
      parallel tasks
    } catch (e) {
      // If there was an exception thrown, the build failed
      throw e
    } finally {
      tasks = [:]
    }
