pipeline {
    agent {
        kubernetes {
            // Define the podTemplate
            podTemplate(label: 'docker', containers: [
                // Define the container with Docker
                containerTemplate(name: 'docker', image: 'docker:latest', command: 'cat', ttyEnabled: true)
            ], volumes: [
                // Define the volume for Docker socket
                hostPathVolume(mountPath: '/var/run/docker.sock', hostPath: '/var/run/docker.sock')
            ])
        }
    }
    stages {
        stage('Build and Test') {
            steps {
                // Run Docker commands within the Docker container
                container('docker') {
                    // Example Docker command
                    sh 'docker version'
                }
            }
        }
    }
}
// pipeline {
//     agent {
//             kubernetes {
//                 yaml '''
//                     apiVersion: v1
//                     kind: Pod
//                     spec:
//                     containers:
//                     - name: docker
//                         image: docker:latest
//                         command:
//                         - cat
//                         tty: true
//                         volumeMounts:
//                         - mountPath: /var/run/docker.sock
//                         name: docker-sock
//                     volumes:
//                     - name: docker-sock
//                         hostPath:
//                         path: /var/run/docker.sock    
//                     '''
//              }
//         }

//     environment {
//         DOCKER_CREDENTIALS = 'Dockerhub-TamDT'
//         DOCKER_IMAGE_NAME = 'tamdt89/demonodejs'
//     }
    
//     stages {
//         stage('Build Docker Image') {
//             steps {
//                 script {
//                     docker.build(DOCKER_IMAGE_NAME, '-f Dockerfile .')
//                 }
//             }
//         }
        
//         stage('Push to Docker Hub') {
//             steps {
//                 script {
//                     docker.withRegistry('https://index.docker.io/v1/', DOCKER_CREDENTIALS) {
//                         docker.image(DOCKER_IMAGE_NAME).push('latest')
//                     }
//                 }
//             }
//         }
//     }
    
//     post {
//         success {
//             echo 'Pipeline executed successfully!'
//         }
//         failure {
//             echo 'Pipeline failed!'
//         }
//     }
// }
