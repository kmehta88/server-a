pipeline {
    agent any
    
    stages {
        stage('Build Docker Image') {
            steps {
                sh 'docker build -t server-a:latest .'
                // Load the freshly built image directly into your kind cluster
                sh 'kind load docker-image server-a:latest --name desktop || true'
            }
        }
        
        stage('Deploy to Kubernetes') {
            steps {
                sh 'kubectl apply -f k8s/deployment.yaml --server=https://host.docker.internal:63829 --insecure-skip-tls-verify=true'
                sh 'kubectl rollout restart deployment/server-a --server=https://host.docker.internal:63829 --insecure-skip-tls-verify=true'
            }
        }
    }
}
