pipeline {
    agent any

    environment {
        IMAGE_NAME = "purushothgit/devops-project"
    }

    stages {

        stage('Clone Repository') {
            steps {
                git 'https://github.com/purushoth-git/devops-k8s-project.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $IMAGE_NAME .'
            }
        }

        stage('Push Docker Image') {
            steps {
                sh 'docker push $IMAGE_NAME'
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                sh 'kubectl apply -f deployment.yaml'
                sh 'kubectl apply -f service.yaml'
            }
        }

    }
}
