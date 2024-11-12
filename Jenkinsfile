pipeline {
    agent any

    tools {
        nodejs 'nodejs'
    }

    environment {
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

        stage('Deploy Application') {
            steps {
                // Dừng các ứng dụng đang chạy trên cổng 3000 (nếu có) trước khi khởi động lại
                sh "lsof -ti:3000 | xargs kill -9 || true"
                // Khởi động ứng dụng
                sh 'nohup npm start &'
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
