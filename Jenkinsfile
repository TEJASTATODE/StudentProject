pipeline {
    agent any
    environment {
        DOCKER_IMAGE = 'your-dockerhub-username/my-django-app' // Change this
    }
    stages {
        stage('Clone Repository') {
            steps {
                script {
                    checkout scm
                }
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                    sh "docker build -t ${DOCKER_IMAGE} ."
                }
            }
        }
        stage('Login to Docker Hub') {
            steps {
                script {
                    withDockerRegistry([credentialsId: 'docker-hub-credentials', url: '']) {
                        echo "Logged in to Docker Hub"
                    }
                }
            }
        }
        stage('Push Docker Image') {
            steps {
                script {
                    sh "docker push ${DOCKER_IMAGE}"
                }
            }
        }
        stage('Run Docker Container') {
            steps {
                script {
                    sh "docker run -d -p 8000:8000 ${DOCKER_IMAGE}"
                }
            }
        }
    }
}
