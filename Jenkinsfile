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