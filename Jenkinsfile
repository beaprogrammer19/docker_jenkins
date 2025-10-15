pipeline {
    agent any

    environment {
        DOCKERHUB_CREDENTIALS = 'dockerhub-creds'
        IMAGE_NAME = 'aditi1903/myapp'
    }

    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/beaprogrammer19/docker_jenkins.git'

            }
        }

        stage('Build and Push Docker Image') {
            steps {
                script {
                    docker.withRegistry('https://index.docker.io/v1/', "${DOCKERHUB_CREDENTIALS}") {
                        def app = docker.build("${IMAGE_NAME}:latest")
                        app.push()
                    }
                }
            }
        }
    }

    post {
        success {
            echo '✅ Docker image built and pushed successfully!'
        }
        failure {
            echo '❌ Build failed. Check logs.'
        }
    }
}


