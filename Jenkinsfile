pipeline {
    agent any

    tools {
        dockerTool 'docker'
    }

    environment {
        DOCKER_IMAGE = 'my-node-app:latest'
    }

    stages {
        stage('Docker Build') {
            steps {
                script {
                    sh 'sudo docker build -t $DOCKER_IMAGE .'
                }
            }
        }
        stage('Docker Run') {
            steps {
                script {
                    sh 'sudo docker run -d -p 3000:3000 $DOCKER_IMAGE'
                }
            }
        }
    }
}