pipeline {
  agent any
  stages {
    stage('Checkout') {
      steps {
        git(url: 'https://github.com/dilmar91/cicd-pipeline', branch: 'main', credentialsId: 'gitPat')
      }
    }

    stage('Build') {
      steps {
        sh './scripts/build.sh'
      }
    }

    stage('Test') {
      steps {
        sh './scripts/test.sh'
      }
    }

    stage('Build Docker Image') {
      steps {
        sh 'docker build -t dilmar91/myapp:${BUILD_NUMBER} .'
      }
    }

    stage('Push Docker Image') {
      steps {
        script {
          docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
            def app = docker.image("dilmar91/myapp:${env.BUILD_NUMBER}")
            app.push("${env.BUILD_NUMBER}")
            app.push("latest")
          }
        }

      }
    }

  }
}