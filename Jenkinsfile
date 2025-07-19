pipeline {
  agent any
  environment {
    VERSION = "1.0.${BUILD_NUMBER}"
  }
  tools {
    maven '3.9.11'
  }
  stages {
    stage('Build') {
      steps {
        echo "Building version ${VERSION}"
        sh 'mkdir -p build && echo "fake build output" > build/output.txt'
      }
    }

    stage('Code Quality (SonarQube)') {
      steps {
        withSonarQubeEnv('LocalSonar') {
          sh 'mvn clean package sonar:sonar'
        }
      }
    }
    
    stage('Archive Artifact') {
      steps {
        archiveArtifacts artifacts: 'build/**/*', fingerprint: true
      }
    }
  }
}
