pipeline {
  agent {
    node {
      label 'jenkins-mvn'
    }

  }
  stages {
    stage('Build') {
      steps {
        sh '''#!/bin/bash
cd $WORKSPACE
ls -al'''
      }
    }

  }
}