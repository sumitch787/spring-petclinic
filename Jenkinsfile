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
cd $WORKSPACE'''
        }

      }
    }

    stage('Build') {
      steps {
        container(name: 'jenkins-mvn') {
          sh 'mvn clean package'
        }

      }
    }

  }
  environment {
    jenkins = 'maven'
  }
}