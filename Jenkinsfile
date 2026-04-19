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
                sh 'docker build -t manasabolla/devops-app:$BUILD_NUMBER ./app'
            }
        }
        stage('Push Image') {
            steps {
                sh 'docker push manasabolla/devops-app:$BUILD_NUMBER'
            }
        }
        stage('Deploy to Kubernetes') {
            steps {
                sh 'kubectl set image deployment/devops-app devops-container=manasabolla/devops-app:$BUILD_NUMBER'
            }
        }
    }
}
