pipeline {
  agent {
    label "img"
  }
  stages {
    stage("Build and push image") {
      steps {
        container('img') {
        sh """
          img build -t gcr.io/core-workshop/ctc-hello-world .
          gcloud auth configure-docker --quiet
          img push gcr.io/core-workshop/ctc-hello-world
        """
        }
      }
    }
  }
}