pipeline {
    agent any

    environment {
        REPO_URL         = 'https://github.com/AydinCY/mind-reader.git'
        CREDENTIALS_ID   = 'github-credentials'
        EMAIL_RECIPIENTS = 'aydincem86@gmail.com'
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: "${REPO_URL}", credentialsId: "${CREDENTIALS_ID}"
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    powershell 'docker build -t mind-reader .'
                }
            }
        }

        stage('Run Tests') {
            steps {
                script {
                    echo 'Running tests...'
                }
            }
        }

        stage('Deploy') {
            steps {
                script {
                    powershell 'docker run -d -p 8082:3000 mind-reader'
                }
            }
        }
    }

    post {
        success {
            echo 'Deployment was successful!'
            // send a success email
            emailext (
              to:      "${EMAIL_RECIPIENTS}",
              subject: "SUCCESS: Job '${env.JOB_NAME} [#${env.BUILD_NUMBER}]'",
              body:    """
                      <p>Good news! The build ${env.JOB_NAME} #${env.BUILD_NUMBER} succeeded.</p>
                      <p>See details at: <a href="${env.BUILD_URL}">${env.BUILD_URL}</a></p>
                      """
            )
        }
        failure {
            echo 'Deployment failed.'
            // send a failure email
            emailext (
              to:      "${EMAIL_RECIPIENTS}",
              subject: "FAILURE: Job '${env.JOB_NAME} [#${env.BUILD_NUMBER}]'",
              body:    """
                      <p>Oops! The build ${env.JOB_NAME} #${env.BUILD_NUMBER} failed.</p>
                      <p>Check console output at: <a href="${env.BUILD_URL}">${env.BUILD_URL}</a></p>
                      """
            )
        }
    }
}
