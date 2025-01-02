pipeline {
    agent any
    stages {
        stage('Clone Repository') {
            steps {
                bat 'git clone https://github.com/abdul-haq350/Docker_Jenkins_Simple_Project.git'
            }
        }
        stage('Install Dependencies') {
            steps {
                bat 'pip install -r requirements.txt'
            }
        }
        stage('Build Docker Image') {
            steps {
                bat 'docker build -t simple-python-app .'
            }
        }
        stage('Push Docker Image') {
            steps {
                bat 'docker login -u <username> -p <password>'
                bat 'docker push simple-python-app'
            }
        }
    }
}
