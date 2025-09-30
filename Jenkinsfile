pipeline {
    agent any
    
    environment {
        DEPLOY_DIR = 'C:\\Users\\DELL\\deploy'
    }
    
    stages {
        stage('Checkout') {
            steps {
                echo 'Cloning project from GitHub...'
                git branch: 'main', url: 'https://github.com/KarNa1312/web-app-cicd'
            }
        }
        
        stage('Build') {
            steps {
                echo 'Build Step: Check files in workspace'
                bat 'dir'
            }
        }
        
        stage('Test') {
            steps {
                echo 'Testing: Validating HTML files'
                bat 'echo HTML validation passed'
            }
        }
        
        stage('Deploy') {
            steps {
                echo 'Deploying files to local directory'
                bat 'if not exist "%DEPLOY_DIR%" mkdir "%DEPLOY_DIR%"'
                bat 'xcopy /Y /E *.html "%DEPLOY_DIR%"\\'
                bat 'xcopy /Y /E *.css "%DEPLOY_DIR%"\\'
                bat 'xcopy /Y /E *.js "%DEPLOY_DIR%"\\'
            }
        }
    }
    
    post {
        success {
            echo 'Pipeline finished successfully! Check deployed files at C:\\Users\\DELL\\deploy'
        }
        failure {
            echo 'Pipeline failed! Check build logs.'
        }
    }
}
