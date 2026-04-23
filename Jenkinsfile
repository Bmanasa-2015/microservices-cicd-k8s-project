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
        stage('Docker Login') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'docker-creds',
                    usernameVariable: 'DOCKER_USER',
                    passwordVariable: 'DOCKER_PASS'
        )]) {
            sh 'echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin'
        }
    }
}
        stage('Push Image') {
            steps {
                sh 'docker push manasabolla/devops-app:$BUILD_NUMBER'
            }
        }
        stage('Deploy to Kubernetes') {
            steps {
                echo 'deploying to kuberenets'
                withKubeConfig([credentialsId: 'kubeconfig']) {
                   
                sh """
                    sed -i 's|yourdockerhub/devops-app:.*|manasabolla/devops-app:${BUILD_NUMBER}|g' k8s/deployment.yaml
                    kubectl  apply -f k8s/deployment.yaml 
                    kubectl apply -f k8s/service.yaml
                   """
            }
        }
    }
}
}
