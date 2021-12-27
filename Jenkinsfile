pipeline {
  agent {
    node {
      label 'jenkins-mvn'
    }

  }
  stages {
    stage('Build') {
      steps {
        container(name: 'jenkins-mvn', shell: 'mvn -v')
      }
    }

  }
  environment {
    jenkins = 'maven'
  }
}