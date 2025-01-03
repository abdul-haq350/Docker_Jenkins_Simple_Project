pipeline {
    agent any
    environment {
        DOCKER_IMAGE = 'abdulhaq2919/simple-python-app:latest'
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
                bat 'docker build -t ${DOCKER_IMAGE} .'
            }
        }
        stage('Push Docker Image') {
            steps {
                script {
                    withCredentials([usernamePassword(credentialsId: 'docker-hub-credentials', usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD')]) {
                        bat """
                            echo ${DOCKER_PASSWORD} | docker login -u ${DOCKER_USERNAME} --password-stdin
                            docker push ${DOCKER_IMAGE}
                        """
                    }
                }
            }
        }
    }
}
