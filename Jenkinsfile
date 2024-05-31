pipeline {
  agent {
    docker { image 'sonarqube:latest' }
  }
  stages {
    stage('Test') {
      steps {
        sh 'sonar-scanner --version' // Example command to test SonarQube version or functionality
      }
    }
  }
}
