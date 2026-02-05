pipeline {
    agent any

    environment {
        IMAGE_NAME = "palmerdevopsapp"
        CONTAINER_NAME = "palmerdevopsapp"
        PORT = "3000"
    }

    stages {
        stage('Checkout') {
            steps {
                // Checkout code from GitHub
                git(
                    url: 'https://github.com/mrAUTHENTIC-18/PALMER-DEVOPS.git',
                    credentialsId: 'github-credentials'
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
                    # Build the Docker image
                    docker build -t $IMAGE_NAME .
                '''
            }
        }

        stage('Run Docker Container') {
            steps {
                sh '''
                    # Run container on port 3000
                    docker run -d -p $PORT:3000 --name $CONTAINER_NAME $IMAGE_NAME
                '''
            }
        }
    }

    post {
        success {
            echo "✅ Palmer DevOps App deployed successfully!"
        }
        failure {
            echo "❌ Deployment failed. Check logs for errors."
        }
    }
}

