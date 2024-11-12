pipeline {
    agent any

    tools {
        nodejs 'nodejs'
        dockerTool 'docker'
    }

    environment {
        DOCKER_IMAGE = 'trongpham99/server-express'
        TELEGRAM_BOT_TOKEN = '7939301771:AAEw4T70jSq7d6JzamJJmPNmBigcExKw3Pk'
        TELEGRAM_CHAT_ID = '-1002394833136'
    }

    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'master', url: 'https://github.com/trongpham99-cpu/server-express.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        // stage('Run Tests') {
        //     steps {
        //         sh 'npm test'
        //     }
        // }
        
        stage('Allow Docker Permissions') {
            steps {
                sh 'sudo chmod 666 /var/run/docker.sock'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh "docker build -t ${DOCKER_IMAGE}:${BUILD_NUMBER} ."
            }
        }

        stage('Push to Docker Hub') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'docker-hub-credentials', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
                    sh 'echo $PASSWORD | docker login -u $USERNAME --password-stdin'
                    sh "docker push ${DOCKER_IMAGE}:${BUILD_NUMBER}"
                }
            }
        }

        stage('Deploy') {
            steps {
                sh "docker run -d -p 3000:3000 ${DOCKER_IMAGE}:${BUILD_NUMBER}"
            }
        }
    }

    post {
        success {
            sendTelegramMessage("✅ Build #${BUILD_NUMBER} was successful! ✅")
        }
        failure {
            sendTelegramMessage("❌ Build #${BUILD_NUMBER} failed. ❌")
        }
    }
}

def sendTelegramMessage(String message) {
    sh """
    curl -s -X POST https://api.telegram.org/bot${TELEGRAM_BOT_TOKEN}/sendMessage \
    -d chat_id=${TELEGRAM_CHAT_ID} \
    -d text="${message}"
    """
}
