pipeline {
    agent any  // Run on Jenkins master (your server)

    stages {
        stage('Checkout') {
            steps {
                checkout scm  // Pulls from GitHub
            }
        }
        stage('Build & Test') {
            steps {
                sh 'npm install'  // Install deps
                sh 'npm test'     // Run tests
            }
        }
        stage('Deploy') {
            steps {
                // Option 1: Simple restart (no Docker)
                sh 'pm2 restart my-app || pm2 start app.js --name my-app'
                
                // Option 2: Docker build & run (uncomment if using)
                // sh 'docker build -t my-app:latest .'
                // sh 'docker stop my-app || true'
                // sh 'docker rm my-app || true'
                // sh 'docker run -d -p 3000:3000 --name my-app my-app:latest'
            }
        }
    }

    post {
        always {
            echo 'Pipeline finished!'
        }
        success {
            echo 'Deployment successful!'
        }
        failure {
            echo 'Build failed!'
        }
    }
}