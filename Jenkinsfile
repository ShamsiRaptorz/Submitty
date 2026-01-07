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
                // Linux command to run docker-compose
                sh 'docker-compose -f docker-compose.yaml build'
            }
        }

        stage('Stop Old Containers') {
            steps {
                echo 'Stopping old containers if any...'
                sh 'docker-compose -f docker-compose.yaml down || true'
            }
        }

        stage('Run Containers') {
            steps {
                echo 'Starting containers...'
                sh 'docker-compose -f docker-compose.yaml up -d'
            }
        }

        stage('Smoke Test') {
            steps {
                echo 'Listing running containers...'
                sh 'docker ps'
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
