pipeline {
  agent {
    label "img"
  } 
  triggers {
    eventTrigger jmespathQuery("tag=='gcr.io/core-workshop/ctc-hello-world:latest'")
  }
  stages {
    stage("Build and push image") {
      when {
          triggeredBy "EventTriggerCause"
          beforeAgent true
      }
      steps {
        container('img') {
          sh """
            img build -t gcr.io/core-workshop/ctc-hello-world-2 .
            gcloud auth configure-docker --quiet
            img push gcr.io/core-workshop/ctc-hello-world-2
          """
        }
      }
    }
  }
}