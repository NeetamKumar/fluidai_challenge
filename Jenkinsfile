pipeline {

    agent any

    stages {

        stage('Checkout') {
            steps {
                git 'https://github.com/NeetamKumar/fluidai_challenge.git'
            }
        }

        stage('Build Image') {
            steps {
                sh 'minikube image build -t fluidai-backend:latest .'
            }
        }

        stage('Deploy') {
            steps {
                sh 'kubectl apply -f k8s/'
            }
        }

        stage('Verify') {
            steps {
                sh 'kubectl rollout status deployment/postgres'
                sh 'kubectl rollout status deployment/backend'
                sh 'kubectl get pods'
            }
        }
    }
}