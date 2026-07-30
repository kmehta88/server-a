pipeline {
    agent any
    
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com//server-a.git'
            }
        }
        
        stage('Build Docker Image') {
            steps {
                sh 'docker build -t server-a:latest .'
            }
        }
        
        stage('Deploy to Kubernetes') {
            steps {
                sh 'kubectl apply -f k8s/deployment.yaml'
                sh 'kubectl rollout restart deployment/server-a'
            }
        }
    }
}
