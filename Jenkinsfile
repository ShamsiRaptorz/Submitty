pipeline {
    agent any

    environment {
        PROJECT_NAME = "Submitty"
    }

    stages {

        stage('Checkout Code') {
            steps {
                echo '📥 Checking out code...'
                git branch: 'main',
                    url: 'https://github.com/ShamsiRaptorz/Submitty.git'
            }
        }

        stage('Build Docker Images') {
            steps {
                echo '🐳 Building Docker images...'
                bat 'docker compose build'
            }
        }

        stage('Stop Existing Containers') {
            steps {
                echo '🛑 Stopping old containers...'
                bat 'docker compose down || exit 0'
            }
        }

        stage('Deploy Containers') {
            steps {
                echo '🚀 Starting containers...'
                bat 'docker compose up -d'
            }
        }

        stage('Smoke Test') {
            steps {
                echo '✅ Running containers:'
                bat 'docker ps'
            }
        }
    }

    post {
        success {
            echo '🎉 Submitty deployment successful!'
        }
        failure {
            echo '❌ Pipeline failed. Check Jenkins logs.'
        }
    }
}
