pipeline {
  agent any
  stages {
    stage('') {
      steps {
        podTemplate(name: 'kuber', namespace: 'jenkins', serviceAccount: 'jenkins', showRawYaml: true)
      }
    }

  }
}