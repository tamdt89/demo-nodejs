pipeline {
    agent { dockerfile true }

    stages {
        stage('Build') {
            steps {
                script {
                    // Xây dựng Docker image
                    docker.build('tamdt89/demonodejs:v1')
                }
            }
        }
        stage('Push') {
            steps {
                script {
                    // Đăng nhập vào Docker Hub
                    docker.withRegistry('https://registry.hub.docker.com', 'tamdtdocker') {
                        // Đẩy Docker image lên Docker Hub
                        docker.image('tamdt89/demonodejs:v1').push('latest')
                    }
                }
            }
        }
    }
}
