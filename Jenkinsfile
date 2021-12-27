pipeline {
  agent {
    node {
      label 'jenkins-mvn'
    }

  }
  stages {
    stage('Build') {
      steps {
        dir(path: '$WORKSPACE')
        sh 'ls -al'
      }
    }

  }
}