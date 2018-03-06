pipeline {
  agent any
  //requires "parameterized-trigger" plug-in installed on Jenkins
  parameters {
    // choices are a string of newline separated values
    // https://issues.jenkins-ci.org/browse/JENKINS-41180
    string( defaultValue: 'jenkinsapp', description: 'Enter the Traffic Manager name', name: 'AZURE_TM_NAME')
    string( defaultValue: 'jenkins', description: 'Enter the Traffic Manager resource group', name: 'AZURE_TM_RESOURCE_GROUP_NAME')
    choice( choices: 'Enabled\nDisabled', description: 'Enter the new desired Traffic Manager status', name: 'TM_STATUS')
    string( defaultValue: 'test', description: 'Enter the enpoint name', name: 'ENDPOINT_NAME')
    choice( choices: 'Enabled\nDisabled', description: 'Select endpoint status', name: 'ENDPOINT_STATUS')
  }
  stages {
    stage('login') {
      steps {
        withCredentials([azureServicePrincipal('azsp4tm')]) {
          sh 'az login --service-principal -u $AZURE_CLIENT_ID -p $AZURE_CLIENT_SECRET -t $AZURE_TENANT_ID'
          sh 'az account set -s $AZURE_SUBSCRIPTION_ID'
          sh 'az resource list'
        }
      }
    }
    stage('Update TM') {
      steps {
        withCredentials([azureServicePrincipal('azsp4tm')]) {
          sh 'az network traffic-manager profile update --name $AZURE_TM_NAME --resource-group $AZURE_TM_RESOURCE_GROUP_NAME --status $TM_STATUS'
        }
      }
    }
    stage('Update EndPoint') {
      steps {
        withCredentials([azureServicePrincipal('azsp4tm')]) {
          sh 'az network traffic-manager endpoint update --name $ENDPOINT_NAME --profile-name $AZURE_TM_NAME --resource-group $AZURE_TM_RESOURCE_GROUP_NAME --type azureEndpoints --endpoint-status $ENDPOINT_STATUS'
        }
      }
    }
  }
}
