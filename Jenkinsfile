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
        volumes:
          - name: docker-sock
            hostPath:
              path: /var/run/docker.sock 
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
  }
    stages {
      stage('Build image') {
        steps {
            container('docker') {
            script {
                sh 'docker build -t tamdt89/demonodejs .'
            }
            }
        }
      }
    }
}