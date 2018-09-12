pipeline {
    agent {
        label "jenkins-nodejs"
    }
    environment {
      ORG               = 'felipeandresceballos'
      APP_NAME          = 'nodejs-test4'
      CHARTMUSEUM_CREDS = credentials('jenkins-x-chartmuseum')
    }
    stages {
      stage('CI Build and push snapshot') {
        environment {
          PREVIEW_VERSION = "0.0.0-SNAPSHOT-$BRANCH_NAME-$BUILD_NUMBER"
          PREVIEW_NAMESPACE = "$APP_NAME-$BRANCH_NAME".toLowerCase()
          HELM_RELEASE = "$PREVIEW_NAMESPACE".toLowerCase()
        }
        steps {
          container('nodejs') {
            sh "npm install"
            sh "uname -a;uptime;df -h"
            sh 'export VERSION=$PREVIEW_VERSION && skaffold build -f skaffold.yaml'
      }
    }
    post {
        always {
            cleanWs()
        }
    }
  }
 }
}
