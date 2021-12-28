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

    stage('Testing') {
      steps {
        container(name: 'jenkins-mvn') {
          sh 'mvn clean verify'
          sh 'mvn test'
        }

      }
    }

    stage('Report') {
      steps {
        container(name: 'jenkins-mvn') {
          jacoco(sourcePattern: '**/target/site/jacoco', execPattern: '**/target/*.exec', buildOverBuild: true, changeBuildStatus: true)
        }

        withSonarQubeEnv('maven') {
          sh 'mvn clean verify $maven'
        }

      }
    }

  }
  environment {
    jenkins = 'maven'
  }
}