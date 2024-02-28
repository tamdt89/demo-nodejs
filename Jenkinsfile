pipeline {
  agent {
    kubernetes {
      yaml '''
        apiVersion: v1
        kind: Pod
        spec:
          containers:
          - name: maven
            image: maven:alpine
            command:
            - cat
            tty: true
          - name: node
            image: node:16-alpine3.12
            command:
            - cat
            tty: true
          - name: docker
            image: docker
            command:
            - cat
            tty: true
          securityContext:
            runAsUser: 10
          volumes:
            - name: docker-sock
              hostPath:
                path: '/var/run/docker.sock'
            '''
    }
  }

  stages {
    stage('Run maven') {
      steps {
        container('maven') {
          sh 'mvn -version'
          sh ' echo Hello World > hello.txt'
          sh 'ls -last'
        }
        container('node') {
          sh 'npm version'
          sh 'cat hello.txt'
          sh 'ls -last'
        }
        container('docker') {
          sh 'docker -v'
          sh 'cat hello.txt'
          sh 'ls -last'
        }
      }
    }
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