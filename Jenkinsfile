pipeline {
    agent any
    environment {
        DOCKER_IMAGE = 'simple-python-app'
        DOCKER_TAG = 'abdulhaq2919/simple-python-app:latest'
        REPO_URL = 'https://github.com/abdul-haq350/Docker_Jenkins_Simple_Project.git'
    }
    stages {
        stage('Clone Repository') {
            steps {
                git "${REPO_URL}"
            }
        }
        stage('Install Dependencies') {
            steps {
                // Ensure Python and pip are installed (check pip version)
                bat 'python -m ensurepip --upgrade'
                bat 'python -m pip install --upgrade pip'
                
                // Create a virtual environment and install requirements
                bat 'python -m venv venv'
                bat 'venv\\Scripts\\activate && pip install -r requirements.txt'
            }
        }
        stage('Build Docker Image') {
            steps {
                bat "docker build -t ${DOCKER_IMAGE} ."
            }
        }
        stage('Push Docker Image') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'docker-hub-credentials', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                    bat "docker login -u ${DOCKER_USER} -p ${DOCKER_PASS}"
                    bat "docker tag ${DOCKER_IMAGE} ${DOCKER_TAG}"
                    bat "docker push ${DOCKER_TAG}"
                }
            }
        }
    }
    post {
        always {
            echo 'Cleaning up workspace...'
            bat "docker rmi ${DOCKER_IMAGE}"
            deleteDir()
        }
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed!'
        }
    }
}
