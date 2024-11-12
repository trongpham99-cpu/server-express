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

        // Uncomment if you want to run tests
        // stage('Run Tests') {
        //     steps {
        //         sh 'npm test'
        //     }
        // }

        stage('Build Application') {
            steps {
                sh 'npm run build' // Hoặc lệnh build phù hợp với dự án của bạn
            }
        }

        stage('Deploy Application') {
            steps {
                // Thực hiện lệnh khởi động ứng dụng, ví dụ với Node.js
                sh 'npm start' // Hoặc lệnh deploy phù hợp
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
