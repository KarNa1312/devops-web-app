pipeline {
    agent any
    
    environment {
        registry = "karna1312/devops-web-app"
        registryCredential = "dockerhub-credentials"
        dockerImage = ""
    }
    
    stages {
        stage('Checkout') {
            steps {
                echo "=== Checking out code from GitHub ==="
                git branch: 'main', url: 'https://github.com/KarNa1312/devops-web-app.git'
            }
        }
        
        stage('Build Docker Image') {
            steps {
                echo "=== Building Docker image ==="
                script {
                    dockerImage = docker.build("${registry}:${env.BUILD_ID}")
                }
            }
        }
        
        stage('Test Image') {
            steps {
                echo "=== Testing Docker image ==="
                bat """
                    docker images | findstr devops-web-app
                    docker run --rm ${registry}:${env.BUILD_ID} nginx -t
                """
            }
        }
        
        stage('Push to Docker Hub') {
            steps {
                echo "=== Pushing image to Docker Hub ==="
                script {
                    docker.withRegistry('https://registry.hub.docker.com', registryCredential) {
                        dockerImage.push("${env.BUILD_ID}")
                        dockerImage.push('latest')
                    }
                }
                echo "=== Image pushed successfully ==="
            }
        }
    }
    
    post {
        always {
            echo "=== Cleaning up Docker resources ==="
            bat 'docker system prune -f || exit 0'
        }
        success {
            echo "=== Pipeline completed successfully ==="
        }
        failure {
            echo "=== Pipeline failed - check logs above ==="
        }
    }
}