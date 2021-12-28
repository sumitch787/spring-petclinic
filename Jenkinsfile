pipeline {
  agent {
    node {
      label 'jenkins-mvn'
    }

  }
  stages {
    stage('Build') {
      steps {
        container(name: 'jenkins-mvn') {
          sh 'cd $WORKSPACE'
          sh 'mvn clean'
          sh 'mvn package'
        }

      }
    }

    stage('Test & Analysis') {
      parallel {
        stage('Test & Analysis') {
          steps {
            container(name: 'jenkins-mvn') {
              withSonarQubeEnv(installationName: 'sonar', envOnly: true, credentialsId: 'sonar') {
                sh 'mvn test sonar:sonar -Dsonar.host.url=$SONAR_HOST_URL -Dsonar.login=$SONAR_AUTH_TOKEN'
              }

            }

          }
        }

        stage('Test') {
          steps {
            container(name: 'jenkins-mvn') {
              sh 'mvn clean verify test'
            }

          }
        }

      }
    }

    stage('Report') {
      steps {
        container(name: 'jenkins-mvn') {
          junit '**/target/surefire-reports/*.html'
          jacoco(buildOverBuild: true, changeBuildStatus: true, execPattern: '**/target/*.exec', sourcePattern: '**/target/site/jacoco-aggregate/*')
        }

      }
    }

    stage('Artifact') {
      steps {
        container(name: 'jenkins-mvn') {
          archiveArtifacts '**/target/*.jar'
        }

      }
    }

  }
  environment {
    jenkins = 'maven'
  }
}