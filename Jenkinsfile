pipeline {
  agent any

  stages {
    stage('Build image') {
      steps {
        container('docker') {
          sh 'docker build -t tamdt89/demonodejs .'
        }
      }
    }
    stage('Push image') {
      steps {
        container('docker') {
          sh 'docker login -u tamdt89 -p DothanhTam'
          sh 'docker push tamdt89/demonodejs'
        }
      }
    }
  }
}