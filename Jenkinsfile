pipeline {
  /*
   * Run everything on an existing agent configured with a label 'agent_maven'.
   */
  agent {
    node {
      label 'agent_maven'
    }
  }

  // using the Timestamper plugin we can add timestamps to the console log
  options {
    timestamps()
  }

  environment {
    //Use Pipeline Utility Steps plugin to read information from pom.xml into env variables
    IMAGE = readMavenPom().getArtifactId()
    VERSION = readMavenPom().getVersion()
  }

  stages {
    stage('Build') {
      steps {
        // using the Pipeline Maven plugin we can set maven configuration settings, publish test results, and annotate the Jenkins console
        echo IMAGE
        echo VERSION
        sh 'mvn install'
      }
    }
  }
  post {
    failure {
      // notify users when the Pipeline fails
      echo "sending email to inform for errors"
    }
    success {
      echo "sending email to inform for success"
    }
  }
}
