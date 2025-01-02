pipeline {
    agent any
    environment {
        DOCKER_IMAGE = 'Docker/simple-python-app:latest'
    }
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
                script {
                    // Docker Hub credentials
                    withCredentials([usernamePassword(credentialsId: 'docker-hub-credentials', usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD')]) {
                        bat """
                            docker login -u ${DOCKER_USERNAME} -p ${DOCKER_PASSWORD}
                            docker tag simple-python-app ${DOCKER_USERNAME}/simple-python-app:latest
                            docker push ${DOCKER_USERNAME}/simple-python-app:latest
                        """
                    }
                }
            }
        }
    }
}
