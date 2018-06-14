//company=odjcompany
// 013

node{
   // Mark the code checkout 'stage'....
   stage 'checkout'

   // Get some code from a GitHub repository
   git url: 'git@github.com:niftyworx/hook-test-basics.git', credentialsId: 'enterprise-bitbucket-key'

   post {
    failure {
      slackSend color: "danger", message: "${env.JOB_NAME} for account ${params.ACCOUNT_NUMBER} has failed!"
    }
    success {
      slackSend color: "good", message: "${env.JOB_NAME} for account ${params.ACCOUNT_NUMBER} has passed!"
    }
  }
   stage 'build'
   //sh 'echo "write your deploy code here";'

   sh whoami
   sh './test.sh'

   stage 'deploy Production'
   //input 'Proceed?'
   //sh 'echo "write your deploy code here"; sleep 6;'
}
