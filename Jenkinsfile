pipeline {
    agent any
    stages {
        stage('Clone Repository') {
            steps {
                git 'https://github.com/abdul-haq350/Docker_Jenkins_Simple_Project.git'
            }
        }
        stage('Check Python') {
            steps {
                bat 'C:\\Users\\abdul\\AppData\\Local\\Programs\\Python\\Python38\\python.exe --version'
            }
        }
        stage('Install Dependencies') {
            steps {
                bat 'C:\\Users\\abdul\\AppData\\Local\\Programs\\Python\\Python38\\python.exe -m pip install --upgrade pip'
                bat 'C:\\Users\\abdul\\AppData\\Local\\Programs\\Python\\Python38\\Scripts\\pip.exe install -r requirements.txt'
            }
        }
        stage('Build Docker Image') {
            steps {
                bat 'docker build -t simple-python-app .'
            }
        }
        stage('Push Docker Image') {
            steps {
                // Push the image directly to Docker Hub without registry if no Docker registry is used
                bat 'docker tag simple-python-app abdulhaq2919/simple-python-app:latest'
                bat 'docker push abdulhaq2919/simple-python-app:latest'
            }
        }
    }
}
