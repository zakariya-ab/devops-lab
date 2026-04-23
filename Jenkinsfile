// pipeline {
//     agent any

//     stages {
//         stage('Clone') {
//             steps {
//                 git branch: 'main',
//                     url: 'https://github.com/zakariya-ab/devops-lab.git'
//             }
//         }
//         stage('Build Docker') {
//             steps {
//                 bat 'docker build -t webapp:latest .'
//             }
//         }
//         stage('DEBUG K8S') {
//             steps {
//                 bat 'kubectl config current-context'
//                 bat 'kubectl get nodes'
//             }
//         }
//         stage('Deploy Kubernetes') {
//             steps {
//                 bat 'kubectl apply -f deployment.yaml'
//                 bat 'kubectl apply -f service.yaml'
//             }
//         }
//     }
// }

pipeline {
    agent any

    environment {
        APP_NAME = "webapp"
        IMAGE_NAME = "webapp"
    }

    stages {

        stage('Clone') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/zakariya-ab/devops-lab.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                bat "docker build -t ${IMAGE_NAME}:${BUILD_NUMBER} ."
            }
        }

        stage('Verify Kubernetes') {
            steps {
                bat "kubectl config current-context"
                bat "kubectl get nodes"
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                script {
                    // Update deployment with new image
                    bat "kubectl set image deployment/${APP_NAME} ${APP_NAME}=${IMAGE_NAME}:${BUILD_NUMBER}"

                    // Wait for rollout to finish
                    bat "kubectl rollout status deployment/${APP_NAME}"
                }
            }
        }

    }
}