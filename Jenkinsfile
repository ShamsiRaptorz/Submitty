pipeline {
    agent any

    environment {
        PROJECT_NAME = "Submitty-CI-CD"
    }

    stages {
        stage('Build Docker Images') {
            steps {
                echo 'Building Docker images...'
                sh 'docker compose build'
            }
        }

        stage('Cleanup Old Containers') {
            steps {
                echo 'Stopping old containers...'
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
                echo 'Checking running containers...'
                sh 'docker ps'
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed!'
        }
    }
}
