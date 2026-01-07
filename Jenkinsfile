pipeline {
    agent any

    stages {
        stage('Build Docker Images') {
            steps {
                echo 'Building Docker images...'
                bat 'docker compose build'
            }
        }

        stage('Cleanup Old Containers') {
            steps {
                echo 'Cleaning up old containers...'
                bat '''
                docker compose down
                exit /b 0
                '''
            }
        }

        stage('Run Containers') {
            steps {
                echo 'Starting containers...'
                bat 'docker compose up -d'
            }
        }

        stage('Smoke Test') {
            steps {
                echo 'Running smoke test...'
                bat 'docker ps'
            }
        }
    }
}
