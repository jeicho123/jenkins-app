pipeline {
  agent any
  environment {
    VERSION = "1.0.${BUILD_NUMBER}"
  }
  stages {
    stage('Build') {
      steps {
        echo "Building version ${VERSION}"
        sh 'mkdir -p build && echo "fake build output" > build/output.txt'
      }
    }
    stage('Archive Artifact') {
      steps {
        archiveArtifacts artifacts: 'build/**/*', fingerprint: true
      }
    }
  }
}
