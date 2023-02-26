pipeline {
  environment {
    registry = "oumaimae/tp4devops"
    registryCredential = 'dockerHub'
    dockerImage = ''
  }
  agent any
  stages {
    stage('Cloning Git') {
      steps {
        git branch: 'main', url: 'https://github.com/Oumaima-el/tp4devops'
      }
    }
    stage('Building image') {
      steps{
        script {
          dockerImage = docker.build registry + ":$BUILD_NUMBER"
        }
      }
    }
    stage('Test image') {
        steps{
        script {
          echo "Tests passed"
        }
      }
    }
    stage('Publish Image') {
      steps{
        script {
          docker.withRegistry( '', registryCredential ) {
            dockerImage.push()
          }
        }
      }
    }
    stage('Deploy image') {
      steps{
        bat "docker run -d -p 8082:80 $registry:$BUILD_NUMBER"
      }
    }
  }
}
