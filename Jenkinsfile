pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                echo 'Checking out source code'
            }
        }

        stage('Check Files') {
            steps {
                bat 'dir'
            }
        }

        stage('Check Docker') {
            steps {
                bat 'docker --version'
            }
        }

        stage('Stop Old Container') {
            steps {
                bat 'docker rm -f nas-server || exit 0'
            }
        }

        stage('Start NAS Container') {
            steps {
                bat 'docker compose up -d'
            }
        }

        stage('Container Status') {
            steps {
                bat 'docker ps'
            }
        }

        stage('Build Report') {
            steps {
                bat 'echo NAS server deployed successfully > build-report.txt'
                bat 'type build-report.txt'
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully'
        }
        failure {
            echo 'Pipeline failed'
        }
    }
}