pipeline {
  agent any
  parameters {
    // requires "parameterized-trigger" installed on Jenkins
    // choice(
    //     // choices are a string of newline separated values
    //     // https://issues.jenkins-ci.org/browse/JENKINS-41180
    //     choices: 'Enabled\nDisabled',
    //     description: 'Enter the new desired status',
    //     name: 'REQUESTED_ACTION')
    // string(
    //     defaultValue: 'jenkinsapp',
    //     description: 'Enter the Traffic Manager name',
    //     name: 'AZURE_TM_NAME')
    booleanParam(name: 'DEBUG_BUILD', defaultValue: true, description: '')
  }
  stages {
    stage('login') {
      steps {
        withCredentials([azureServicePrincipal('azsp4tm')]) {
          sh 'az login --service-principal -u $AZURE_CLIENT_ID -p $AZURE_CLIENT_SECRET -t $AZURE_TENANT_ID'
          sh 'az account set -s $AZURE_SUBSCRIPTION_ID'
          sh 'az resource list'
          sh 'az network traffic-manager profile update --name $AZURE_TM_NAME --resource-group $AZURE_TM_RESOURCE_GROUP_NAME --status $REQUESTED_ACTION 
        }
      }
    }
  }
}
