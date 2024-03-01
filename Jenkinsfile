pipeline {
environment {
registry = "tamdt89/demonodejs"
registryCredential = 'tamdtdocker'
dockerImage = ''
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

// pipeline {
//     agent { dockerfile true }

//     stages {
//         stage('Build') {
//             steps {
//                 script {
//                     // Xây dựng Docker image
//                     docker.build('tamdt89/demonodejs:v1')
//                 }
//             }
//         }
//         stage('Push') {
//             steps {
//                 script {
//                     // Đăng nhập vào Docker Hub
//                     withDockerRegistry(credentialsId: 'tamdtdocker', url: 'https://index.docker.io/v1/') {
//                        docker.image('tamdt89/demonodejs:v1').push('v1')
//                     }
//                     // docker.withRegistry('https://registry.hub.docker.com', 'tamdtdocker') {
//                     //     // Đẩy Docker image lên Docker Hub
//                     //     docker.image('tamdt89/demonodejs:v1').push('v1')
//                     // }
//                 }
//             }
//         }
//     }
// }
