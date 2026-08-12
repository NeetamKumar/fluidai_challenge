pipeline {
    agent any

    stages {

        stage('Debug Environment') {
            steps {
                sh '''
                    whoami
                    echo "HOME=$HOME"
                    which minikube
                    which kubectl
                    minikube profile list
                    minikube status
                    kubectl get nodes
                '''
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
