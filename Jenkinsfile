pipeline {
    agent any

    stages {
        stage('Clone') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/zakariya-ab/devops-lab.git'
            }
        }
        stage('Build Docker') {
            steps {
                bat 'docker build -t webapp:latest .'
            }
        }
        stage('DEBUG K8S') {
            steps {
                bat 'kubectl config current-context'
                bat 'kubectl get nodes'
            }
        }
        stage('Deploy Kubernetes') {
            steps {
                bat 'kubectl apply -f deployment.yaml'
                bat 'kubectl apply -f service.yaml'
            }
        }
    }
}