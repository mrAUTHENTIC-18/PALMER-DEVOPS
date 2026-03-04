pipeline {
    agent any

    environment {
        GIT_REPO = "https://github.com/mrAUTHENTIC-18/PALMER-DEVOPS.git"
        GIT_BRANCH = "main"
        GIT_CREDENTIALS = "github-credentials"
    }

    stages {

        stage('Checkout') {
            steps {
                git(
                    url: env.GIT_REPO,
                    branch: env.GIT_BRANCH,
                    credentialsId: env.GIT_CREDENTIALS
                )
            }
        }

        stage('Clean Previous Deployment') {
            steps {
                sh '''
                    echo "Stopping existing containers..."
                    docker-compose down || true
                '''
            }
        }

        stage('Build Docker Images') {
            steps {
                sh '''
                    echo "Building Docker images..."
                    docker-compose build
                '''
            }
        }

        stage('Deploy Application') {
            steps {
                sh '''
                    echo "Starting containers..."
                    docker-compose up -d
                '''
            }
        }

        stage('Verify Deployment') {
            steps {
                sh 'docker ps'
            }
        }
    }

    post {
        success {
            echo "✅ Palmer DevOps App deployed successfully with Docker Compose!"
        }
        failure {
            echo "❌ Deployment failed. Check logs for errors."
        }
    }
}