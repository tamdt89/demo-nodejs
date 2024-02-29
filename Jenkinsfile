pipeline {
    agent { dockerfile true }
    stages {
        stage('Test') {
            steps {
                sh 'node --version'
                sh 'svn --version'
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
