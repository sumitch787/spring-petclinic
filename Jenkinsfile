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
      parallel {
        stage('Build') {
          steps {
            container(name: 'jenkins-mvn') {
              sh 'mvn clean package'
            }

          }
        }

        stage('Test') {
          steps {
            container(name: 'jenkins-mvn') {
              sh 'mvn clean test'
            }

          }
        }

      }
    }

  }
  environment {
    jenkins = 'maven'
  }
}