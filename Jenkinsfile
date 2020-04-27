/* name: Jenkinsfile Groovy Pipeline - Nationwide Building Society - Landing Zones
   created: May 25, 2019
   Author: Mark McLEod
   Revisions: Mark McLeod (4/06/2019)  - Fix account discovery and implement 'Initialise' Stage
              Mark McLeod (5/06/2019)  - Review, JavaDoc and remove redundent code
              Mark McLeod (11/06/2019) - Changes to Slack notifications and try,catch,finally
*/

  /*
    Global Environment Variables
  */
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
      //Initialise what needs to be built and checkout the SCM
      checkout scm
      //Find all of the accounts in the management OU only, for now
      builds = org.getListOrgAccts()
      //remove the master account, this is built only once to initialise the landing zone
      echo "Pipeline - Landing Zone Accounts: ${builds}"
      awsIdentity()
    }

  /*
    Testing stage: Run on all branches
                   Terraform actions (test => Init, fmt, validate)
  */
  stage 'Lint'
    //Loop through all accounts found and build a paralle task for each
    for(String item: builds) {
      def account_path = item
      tasks["${item}"] = {
        node {
          //Each node is in a seperate folder, possiblly a seperate agent, need to checkout the SCM
          checkout scm
          withAWS(region:"${env.REGION}",credentials:"${env.CREDS}", role:"cloud-team-admin", roleAccount:"${item}", externalId: "cloud-team-admin") {
            validateTemplates()
          }
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
