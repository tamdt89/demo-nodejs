pipeline {
    agent any
    
    environment {
        DOCKER_CREDENTIALS = 'Dockerhub-TamDT'
        DOCKER_IMAGE_NAME = 'tamdt89/demonodejs'
    }
    
    stages {
        stage('Build Docker Image') {
            steps {
                script {
                    docker.build(DOCKER_IMAGE_NAME, '-f Dockerfile .')
                }
            }
        }
        
        stage('Push to Docker Hub') {
            steps {
                script {
                    docker.withRegistry('https://index.docker.io/v1/', DOCKER_CREDENTIALS) {
                        docker.image(DOCKER_IMAGE_NAME).push('latest')
                    }
                }
            }
        }
    }
    
    post {
        success {
            echo 'Pipeline executed successfully!'
        }
        failure {
            echo 'Pipeline failed!'
        }
    }
}
