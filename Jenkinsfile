pipeline {
  agent any
  stages {
    stage('Checkout') {
      steps {
        git(url: 'https://github.com/dilmar91/cicd-pipeline', branch: 'main', credentialsId: 'gitPat')
      }
    }

  }
}