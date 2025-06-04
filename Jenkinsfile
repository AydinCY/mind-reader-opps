pipeline {
    agent any

    environment {
        REPO_URL = 'https://github.com/yourusername/mind-reader.git'  // Your main repo URL
    }

    stages {
        stage('Checkout') {
            steps {
                // Clone the mind-reader repository
                git branch: 'main', url: "${REPO_URL}"
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    // Use PowerShell for Windows, instead of 'sh' for Linux/macOS
                    powershell 'docker build -t mind-reader .'
                }
            }
        }

        stage('Run Tests') {
            steps {
                script {
                    // Optional: You can add tests here (e.g., running unit tests, static checks)
                    echo 'Running tests...'
                }
            }
        }

        stage('Deploy') {
            steps {
                script {
                    // Use PowerShell for Windows, instead of 'sh' for Linux/macOS
                    powershell 'docker run -d -p 8080:80 mind-reader'
                }
            }
        }
    }

    post {
        success {
            echo 'Deployment was successful!'
        }
        failure {
            echo 'Deployment failed.'
        }
    }
}
