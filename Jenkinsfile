pipeline {
  agent {
    node {
      label 'jenkins-mvn'
    }

  }
  stages {
    stage('Checkout') {
      steps {
        container(name: 'jenkins-mvn') {
          sh 'mvn -v'
        }

      }
    }

  }
  environment {
    jenkins = 'maven'
  }
}