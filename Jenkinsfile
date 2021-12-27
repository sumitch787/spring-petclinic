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
          sh '''pwd 
cd $WORKSPACE
ls -al'''
        }

      }
    }

  }
  environment {
    jenkins = 'maven'
  }
}