pipeline {
  environment {
    registry = "piyushoswal1989/docker_builds"
    registryCredentials = "62eaeaf6-4154-47c0-9148-4566558cdbfa"
    dockerImage = ''
  }
  
  agent any
  
  stages {
    stage('Build Docker Image') {
      steps {
        script {
          dockerImage = docker.build registry + ":$BUILD_NUMBER"
        }
      }
    }
    stage('Push to DockerHub') {
      steps {
        script  {
          docker.withRegistry('',registryCredentials)  {
            docker.Image.push()
          }
        }
      }
    }
    stage('Test Run') {
      steps {
        sh 'docker run -d $registry:$BUILD_NUMBER'
      }
    }
  }
}
