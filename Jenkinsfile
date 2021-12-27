pipeline {
  agent {
    node {
      label 'jenkins-mvn'
    }

  }
  stages {
    stage('build') {
      steps {
        sh '''pwd \\
cd  $WORKSPACE \\
mvn -v'''
      }
    }

  }
}