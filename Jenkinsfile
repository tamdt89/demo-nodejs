pipeline {
environment {
registry = "tamdt89/demonodejs"
registryCredential = 'tamdtdocker'
dockerImage = ''
BUILD_NUMBER='1'
}
agent any
    stages {
        // stage('Cloning our Git') {
        //     steps {
        //         git 'https://github.com/tamdt89/demo-nodejs.git'
        //     }
        // }
        stage('Building our image') {
            steps{
                script {
                    dockerImage = docker.build registry + ":$BUILD_NUMBER"
                }
            }
        }
        stage('Deploy our image') {
            steps{
                script {
                    docker.withRegistry( '', registryCredential ) {
                    dockerImage.push()
                    }   
                }
            }
        }
        stage('Cleaning up') {
            steps{
                sh "docker rmi $registry:$BUILD_NUMBER"
            }
        }
    }
}

