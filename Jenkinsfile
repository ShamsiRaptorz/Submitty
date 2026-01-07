pipeline {
    agent any

    environment {
        PROJECT_NAME = "Submitty"
    }

    stages {
        stage('Checkout Code') {
            steps {
                echo 'Checking out code from GitHub...'
                git url: 'https://github.com/ShamsiRaptorz/Submitty.git', branch: 'main'
            }
        }

        stage('Build Docker Images') {
            steps {
                echo 'Building Docker images...'
                // Windows command to run docker-compose
                bat 'docker compose -f docker-compose.yaml build'
            }
        }

        stage('Stop Old Containers') {
            steps {
                echo 'Stopping old containers if any...'
                bat 'docker compose -f docker-compose.yaml down || exit 0'
            }
        }

        stage('Run Containers') {
            steps {
                echo 'Starting containers...'
                bat 'docker compose -f docker-compose.yaml up -d'
            }
        }

        stage('Smoke Test') {
            steps {
                echo 'Listing running containers...'
                bat 'docker ps'
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed. Check logs for errors.'
        }
    }
}
