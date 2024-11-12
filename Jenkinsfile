pipeline {
    agent any

    tools {
        nodejs 'Node 14' // Use the name you configured in Jenkins
    }

    environment {
        DOCKER_IMAGE = 'my-node-app:latest'
    }

    stages {
        stage('Build') {
            steps {
                script {
                    sh 'npm install'
                }
            }
        }
        stage('Test') {
            steps {
                script {
                    sh 'npm test' // Modify this if you have tests
                }
            }
        }
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
                    sh 'docker run -d -p 3000:3000 $DOCKER_IMAGE'
                }
            }
        }
    }
}

