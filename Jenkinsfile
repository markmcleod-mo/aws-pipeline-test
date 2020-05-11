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
