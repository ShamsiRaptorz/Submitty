pipeline {
    agent any

    stages {
        stage('Build Docker Images') {
            steps {
                echo 'Building Docker images...'
                sh 'docker compose build'
            }
        }

        stage('Cleanup Old Containers') {
            steps {
                echo 'Cleaning up old containers...'
                sh 'docker compose down || true'
            }
        }

        stage('Run Containers') {
            steps {
                echo 'Starting containers...'
                sh 'docker compose up -d'
            }
        }

        stage('Smoke Test') {
            steps {
                echo 'Running smoke test...'
                sh 'docker ps'
            }
        }
    }
}
