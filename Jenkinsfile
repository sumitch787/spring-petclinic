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
          sh 'mvn compile'
          sh 'mvn install'
          sh 'mvn verify'
        }

      }
    }

    stage('Test & Analysis') {
      parallel {
        stage('sonar') {
          steps {
            container(name: 'jenkins-mvn') {
              withSonarQubeEnv(installationName: 'sonar', envOnly: true, credentialsId: 'sonar') {
                sh 'mvn test sonar:sonar -Dsonar.host.url=$SONAR_HOST_URL -Dsonar.login=$SONAR_AUTH_TOKEN'
              }

            }

          }
        }

        stage('checkstyle') {
          steps {
            container(name: 'jenkins-mvn') {
              sh 'mvn checkstyle:checkstyle'
            }

          }
        }

      }
    }

    stage('Report') {
      steps {
        container(name: 'jenkins-mvn') {
          junit '**/target/site/*.html'
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