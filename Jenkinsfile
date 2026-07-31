pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/Katukuri-Sai-Prathyusha/cicd.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t cicd-app .'
            }
        }

        stage('Stop Old Container') {
            steps {
                sh 'docker stop cicd-app || true'
                sh 'docker rm cicd-app || true'
            }
        }

        stage('Run Container') {
            steps {
                sh 'docker run -d --name cicd-app -p 3000:3000 cicd-app'
            }
        }
    }
}
