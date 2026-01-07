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
                sh 'docker compose build'
            }
        }

        stage('Stop Existing Containers') {
            steps {
                echo '🛑 Stopping old containers...'
                sh 'docker compose down || true'
            }
        }

        stage('Deploy Containers') {
            steps {
                echo '🚀 Starting containers...'
                sh 'docker compose up -d'
            }
        }

        stage('Smoke Test') {
            steps {
                echo '✅ Running containers:'
                sh 'docker ps'
            }
        }
    }

    post {
        success {
            echo '🎉 Submitty deployment successful!'
        }
        failure {
            echo '❌ Pipeline failed. Check logs.'
        }
    }
}
