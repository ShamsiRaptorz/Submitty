pipeline {
    agent any

    stages {

        stage('Build Docker Images') {
            steps {
                bat 'docker compose build'
            }
        }

        stage('Cleanup Old Containers') {
            steps {
                bat 'docker compose down || exit 0'
            }
        }

        stage('Run Containers') {
            steps {
                bat 'docker compose up -d'
            }
        }

        stage('Smoke Test') {
            steps {
                bat 'docker ps'
            }
        }
    }
}
