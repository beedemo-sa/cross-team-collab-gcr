pipeline {
  agent none
  triggers {
    eventTrigger jmespathQuery("subscription=='projects/core-workshop/subscriptions/core-demo'")
  }
  stages {
    stage('Decode JSON payload') {
      agent any
      when {
        triggeredBy "EventTriggerCause"
        beforeAgent true
      }
      steps {
        script {
          data = currentBuild?.getBuildCauses()[0]?.event?.message?.data?.toString()
          event = sh(returnStdout: true, script: "echo ${data} | base64 -d").trim()
        }
        echo event
      }
    }
    stage('Publish event') {
      agent none
      when {
        triggeredBy "EventTriggerCause"
        beforeAgent true
      }
      steps {
        publishEvent event: jsonEvent(event), verbose: true
      }
    }
  }
}