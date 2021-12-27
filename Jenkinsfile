pipeline {
  agent {
    node {
      label 'jenkins-mvn'
    }

  }
  stages {
    stage('Build') {
      parallel {
        stage('Build') {
          steps {
            sh '''#!/bin/bash
cd $WORKSPACE

'''
          }
        }

        stage('Checking Maven Version') {
          steps {
            sh 'mvn -v'
          }
        }

        stage('Clean Package') {
          steps {
            sh 'mvn clean package'
          }
        }

      }
    }

  }
  environment {
    jenkins = 'maven'
  }
}