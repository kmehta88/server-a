pipeline {
    agent any
    
    stages {
        stage('Build Docker Image') {
            steps {
                sh 'docker build -t server-a:latest .'
            }
        }
        
        stage('Deploy to Kubernetes') {
            steps {
                // Pass host.docker.internal and disable TLS verification for local dev
                sh 'kubectl apply -f k8s/deployment.yaml --server=https://host.docker.internal:63829 --insecure-skip-tls-verify=true'
                sh 'kubectl rollout restart deployment/server-a --server=https://host.docker.internal:63829 --insecure-skip-tls-verify=true'
            }
        }
    }
}
