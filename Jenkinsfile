pipeline {
    agent any
    stages {
        stage('Clone') {
            steps {
                checkout scm
            }
        }
        stage('Build Docker Image') {
            steps {
                sh 'docker build -t yourdockerhub/devops-app:$BUILD_NUMBER ./app'
            }
        }
        stage('Push Image') {
            steps {
                sh 'docker push yourdockerhub/devops-app:$BUILD_NUMBER'
            }
        }
        stage('Deploy to Kubernetes') {
            steps {
                sh 'kubectl set image deployment/devops-app devops-container=yourdockerhub/devops-app:$BUILD_NUMBER'
            }
        }
    }
}
