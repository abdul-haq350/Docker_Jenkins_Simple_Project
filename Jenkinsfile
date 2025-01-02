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
        bat 'C:\\Python38\\python.exe --version'  // Use full path to python.exe
    }
}
stage('Install Dependencies') {
    steps {
        bat 'C:\\Python38\\python.exe -m pip install --upgrade pip'
        bat 'C:\\Python38\\Scripts\\pip.exe install -r requirements.txt'
    }
}
        stage('Check Environment Variables') {
    steps {
        bat 'echo %PATH%'
        bat 'python --version'
    }
}

        stage('Build Docker Image') {
            steps {
                bat 'docker build -t simple-python-app .'
            }
        }
        stage('Push Docker Image') {
            steps {
                withDockerRegistry([credentialsId: 'docker-hub-credentials', url: '']) {
                    bat 'docker tag simple-python-app abdulhaq2919/simple-python-app:latest'
                    bat 'docker push abdulhaq2919/simple-python-app:latest'
                }
            }
        }
    }
}
