#!groovy
pipeline {
  agent any
  options {
    timeout(time: 1, unit: 'HOURS')
    timestamps()
    disableConcurrentBuilds()
  }
  stages {
    stage('Checkout SCM') {
      steps {
            dir('hook-test-basics') {
              git url: 'git@github.com:niftyworx/hook-test-basics.git', credentialsId: 'enterprise-bitbucket-key'
            }
      }
    }

    stage('2nd Stage') {
      steps {
        dir('hook-test-basics') {
          sh 'echo 2nd stage'
        }
      }
    }
    // stage('Trigger Dev Deployment') {
    //   when {
    //     equals expected: '091036132616', actual: "${params.ACCOUNT_NUMBER}"
    //   }
    //   steps {
    //     build job: 'deployment', parameters: [
    //       [$class: 'StringParameterValue', name: 'REGION', value: "${params.REGION}"],
    //       [$class: 'StringParameterValue', name: 'ACCOUNT_NUMBER', value: "${params.ACCOUNT_NUMBER}"],
    //       [$class: 'StringParameterValue', name: 'DEPLOYMENT_TYPE', value: 'app']
    //     ]
    //   }
    // }
  }
  post {
    failure {
      slackSend color: "danger", message: "env.JOB_NAME for account params.ACCOUNT_NUMBER has failed!"
    }
    success {
      slackSend color: "good", message: "env.JOB_NAME for account params.ACCOUNT_NUMBER has passed!"
    }
  }
}
