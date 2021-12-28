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
          dir(path: '$WORKSPACE')
        }

      }
    }

    stage('Build') {
      parallel {
        stage('Test') {
          steps {
            container(name: 'jenkins-mvn') {
              withSonarQubeEnv(installationName: 'sonar', envOnly: true, credentialsId: 'sonar') {
                sh '"env"'
                sh '''mvn test sonar:sonar -Dsonar.host.url=$SONAR_HOST_URL \\ 
-Dsonar.login=$SONAR_AUTH_TOKEN \\
-Dsonar.projectKey=$SONAR_PROJECT_KEY'''
              }

            }

          }
        }

        stage('build') {
          steps {
            container(name: 'jenkins-mvn') {
              sh 'mvn package'
            }

          }
        }

        stage('Clean') {
          steps {
            container(name: 'jenkins-mvn') {
              sh 'mvn clean'
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