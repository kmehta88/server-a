pipeline {
    agent any
    
    stages {
        stage('Build & Push to Local Registry') {
            steps {
                sh 'docker build -t host.docker.internal:5001/server-a:latest .'
                sh 'docker push host.docker.internal:5001/server-a:latest'
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
