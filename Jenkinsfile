pipeline {
    agent any
 
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
    }
    post {
        always {
            cleanWs()
        }
    }
}
