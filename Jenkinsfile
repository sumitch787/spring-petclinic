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
        stage('test') {
          steps {
            container(name: 'jenkins-mvn') {
              withSonarQubeEnv(installationName: 'maven', envOnly: true) {
                sh 'echo ${SONAR_HOST_URL}'
              }

              sh 'mvn test sonar:sonar -Dsonar.host.url=$SONAR_HOST_URL -Dsonar.login=$SONAR_AUTH_TOKEN'
            }

          }
        }

        stage('Build') {
          steps {
            container(name: 'jenkins-mvn') {
              sh 'mvn clean package '
            }

          }
        }

      }
    }

    stage('Reports') {
      steps {
        container(name: 'jenkins-mvn') {
          junit '**/target/surefire-reports/*.html'
          jacoco(buildOverBuild: true, changeBuildStatus: true, execPattern: '**/target/*.exec', sourcePattern: '**/target/site/jacoco-aggregate/*')
          findBuildScans()
        }

      }
    }

  }
  environment {
    jenkins = 'maven'
  }
}