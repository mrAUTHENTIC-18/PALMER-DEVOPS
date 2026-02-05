pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                git credentialsId: 'github-credentials', url: 'https://github.com/mrAUTHENTIC-18/PALMER-DEVOPS.git', branch: 'main'
            }
        }
        stage('Build Docker Image') {
            steps {
                sh 'docker build -t palmer-devops-app .'
            }
        }
        stage('Deploy Docker Container') {
            steps {
                sh '''
                docker stop palmer-devops-app || true
                docker rm palmer-devops-app || true
                docker run -d -p 3000:3000 --name palmer-devops-app palmer-devops-app
                '''
            }
        }
    }
}

