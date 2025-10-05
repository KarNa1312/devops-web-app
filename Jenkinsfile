pipeline {
    agent any
    
    environment {
        registry = "karna1312/devops-web-app"
        BUILD_TAG = "${env.BUILD_ID}"
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
                bat """
                    docker build -t ${registry}:${BUILD_TAG} .
                    docker tag ${registry}:${BUILD_TAG} ${registry}:latest
                """
                echo "=== Image built successfully ==="
            }
        }
        
        stage('Verify Image') {
            steps {
                echo "=== Verifying Docker image ==="
                bat """
                    docker images | findstr ${registry}
                    echo Image verified successfully!
                """
            }
        }
        
        stage('Push to Docker Hub') {
            steps {
                echo "=== Pushing image to Docker Hub ==="
                withCredentials([usernamePassword(credentialsId: 'dockerhub-credentials', passwordVariable: 'DOCKER_PASS', usernameVariable: 'DOCKER_USER')]) {
                    bat """
                        echo %DOCKER_PASS% | docker login -u %DOCKER_USER% --password-stdin
                        docker push ${registry}:${BUILD_TAG}
                        docker push ${registry}:latest
                        docker logout
                    """
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
            echo "=== CI/CD Pipeline completed successfully ==="
        }
        failure {
            echo "=== Pipeline failed - check logs above ==="
        }
    }
}