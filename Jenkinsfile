pipeline {
  agent any
  stages {
    stage('login') {
      steps {
        sh 'sh tmscript.sh'
      }
    }
  }
  parameters {
    choice(choices: '''enable
disable''', description: 'Enter the new desired status', name: 'REQUESTED_ACTION')
  }
}