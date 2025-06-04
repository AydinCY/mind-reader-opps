pipeline {
    agent any

    environment {
        REPO_URL = 'https://github.com/AydinCY/mind-reader.git'  // Your main repo URL
        CREDENTIALS_ID = 'github-credentials' // This is the ID of the credentials you created for GitHub
    }

    stages {
        stage('Checkout') {
            steps {
                // Clone the mind-reader repository using the configured credentials
                git branch: 'main', url: "${REPO_URL}", credentialsId: "${CREDENTIALS_ID}"
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    // Build the Docker image for the app
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
                    // Run the Docker container, exposing port 3000 inside the container to 8080 on the host
                    powershell 'docker run -d -p 8080:3000 mind-reader'
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
