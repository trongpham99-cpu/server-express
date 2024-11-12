pipeline {
    agent any

    environment {
        NODE_ENV = 'production'
    }

    tools {
        nodejs 'nodejs'
    }

    stages {
        stage('Install Dependencies') {
            steps {
                script {
                    sh 'npm install'
                }
            }
        }
        stage('Run Tests') {
            steps {
                script {
                    sh 'npm test'
                }
            }
        }
        stage('Start Application') {
            steps {
                script {
                    sh 'npm start'
                }
            }
        }
    }
}