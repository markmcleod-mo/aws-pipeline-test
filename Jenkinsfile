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
      env.REGION = 'eu-west-2'
      env.CREDS = 'test-master'
      //Initialise what needs to be built and checkout the SCM
      checkout scm
      //Find all of the accounts in the management OU only, for now
      accounts = org.getListOrgAccts("005402609678", "cloud-team-admin", "MGMT")
      //builds = ['327472442310','881927508427','892305036901','005402609678','170090038151','172335553610']
      echo "Pipeline - : ${accounts}"
      //awsIdentity()
    }

  stage 'Lint'
    //Loop through all accoun  ts found and build a paralle task for each
    for(String item: accounts) {
      def account_path = item
      tasks["${item}"] = {
        node {
          echo "account_path=${account_path}"
          //Each node is in a seperate folder, possiblly a seperate agent, need to checkout the SCM
          checkout scm
          //withAWS(region:"${env.REGION}",credentials:"${env.CREDS}", role:"cloud-team-admin", roleAccount:"${item}", externalId: "cloud-team-admin") {
            validateTemplates("./", "${account_path}", "cloud-team-admin")
          //}
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
