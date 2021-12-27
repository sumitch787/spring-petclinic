pipeline {
  agent {
    node {
      label 'jenkins-mvn'
    }

  }
  stages {
    stage('build') {
      steps {
        sh '''pwd
cd  ${env.WORKSPACE}
mvn -v'''
      }
    }

  }
}