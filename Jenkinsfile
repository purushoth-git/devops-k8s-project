pipeline {
    agent any

    environment {
        IMAGE_NAME = "purushothdoc/devops-project:latest"
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
        withCredentials([usernamePassword(credentialsId: 'dockerhub', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
            sh 'echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin'
            sh 'docker push purushothdoc/devops-project:latest'
        }
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
