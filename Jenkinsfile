pipeline {
    agent any
    
    environment {
        // Đặt các biến môi trường cần thiết, như tên image và tag
        DOCKER_REGISTRY = "docker.io" // Địa chỉ Docker registry, ở đây là Docker Hub
        DOCKER_USERNAME = credentials('tamdt-dockerhub') // Tên đăng nhập Docker Hub (sử dụng Jenkins credentials)
        DOCKER_PASSWORD = credentials('tamdt-dockerhub') // Mật khẩu Docker Hub (sử dụng Jenkins credentials)
        IMAGE_NAME = "demonodejs" // Tên của image
        IMAGE_TAG = "latest" // Tag của image
    }
    
    stages {
        stage('Build') {
            steps {
                // Bước này sẽ build image từ Dockerfile
                script {
                    docker.build("${DOCKER_REGISTRY}/${DOCKER_USERNAME}/${IMAGE_NAME}:${IMAGE_TAG}", ".")
                }
            }
        }
        stage('Push') {
            steps {
                // Đăng nhập vào Docker Hub
                script {
                    docker.withRegistry("${DOCKER_REGISTRY}", "${DOCKER_USERNAME}", "${DOCKER_PASSWORD}") {
                        // Bước này sẽ push image lên Docker Hub
                        docker.image("${DOCKER_USERNAME}/${IMAGE_NAME}:${IMAGE_TAG}").push()
                    }
                }
            }
        }
    }
}
