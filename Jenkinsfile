pipeline {
    agent any

    tools {
        nodejs 'nodejs'
    }

    environment {
        DOCKER_IMAGE = 'my-node-app:latest'
    }

    stages {
        stage('Docker Build') {
            steps {
                script {
                    sh 'docker build -t $DOCKER_IMAGE .'
                }
            }
        }
        stage('Docker Run') {
            steps {
                script {
                    sh 'docker run -d -p 3004:3000 $DOCKER_IMAGE'
                }
            }
        }
    }
}

