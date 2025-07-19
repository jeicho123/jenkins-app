pipeline {
  agent any
  environment {
    VERSION = "1.0.${BUILD_NUMBER}"
  }
  tools {
    maven 'maven'
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
