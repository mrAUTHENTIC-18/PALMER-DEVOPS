pipeline {
    agent any

    environment {
        IMAGE_NAME = "palmerdevopsapp"
        CONTAINER_NAME = "palmerdevopsapp"
        PORT = "3000"
        GIT_REPO = "https://github.com/mrAUTHENTIC-18/PALMER-DEVOPS.git"
        GIT_BRANCH = "main"  // Make sure this matches your GitHub default branch
        GIT_CREDENTIALS = "github-credentials"
    }

    stages {
        stage('Checkout') {
            steps {
                // Pull latest code from GitHub
                git(
                    url: env.GIT_REPO,
                    branch: env.GIT_BRANCH,
                    credentialsId: env.GIT_CREDENTIALS
                )
            }
        }

        stage('Clean Previous Containers') {
            steps {
                sh '''
                    # Stop old container if exists
                    docker stop $CONTAINER_NAME || true
                    # Remove old container if exists
                    docker rm $CONTAINER_NAME || true
                    # Remove unused Docker networks
                    docker network prune -f
                '''
            }
        }

        stage('Build Docker Image') {
            steps {
                sh '''
                    # Build Docker image
                    docker build -t $IMAGE_NAME .
                '''
            }
        }

        stage('Run Docker Container') {
            steps {
                sh '''
