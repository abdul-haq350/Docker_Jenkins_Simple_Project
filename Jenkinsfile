pipeline {
    agent any
    stages {
        stage('Clone Repository') {
            steps {
                git 'https://github.com/abdul-haq350/Docker_Jenkins_Simple_Project.git'
            }
        }
        stage('Install Dependencies') {
            steps {
                sh 'pip install -r requirements.txt'
            }
        }
        stage('Build Docker Image') {
            steps {
                sh 'docker build -t simple-python-app .'
            }
        }
        stage('Push Docker Image') {
            steps {
                withDockerRegistry([credentialsId: 'docker-hub-credentials', url: '']) {
                    sh 'docker tag simple-python-app abdulhaq2919/simple-python-app:latest'
                    sh 'docker push abdulhaq2919/simple-python-app:latest'
                }
            }
        }
    }
}
