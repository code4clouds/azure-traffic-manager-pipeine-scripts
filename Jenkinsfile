pipeline {
  agent any
  parameters {
    // requires "parameterized-trigger" installed on Jenkins
    choice(
        // choices are a string of newline separated values
        // https://issues.jenkins-ci.org/browse/JENKINS-41180
        choices: 'enable\ndisable',
        description: 'Enter the new desired status',
        name: 'REQUESTED_ACTION')
  }
  stages {
    stage('login') {
      withCredentials([azureServicePrincipal('principal-credentials-id')]) {
        sh 'az login --service-principal -u $AZURE_CLIENT_ID -p $AZURE_CLIENT_SECRET -t $AZURE_TENANT_ID'
        sh 'az account set -s $AZURE_SUBSCRIPTION_ID'
        sh 'az resource list'
      }
    }
  }

}