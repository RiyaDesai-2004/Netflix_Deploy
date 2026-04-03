pipeline {
    agent any

    environment {
        IMAGE_NAME = "netflix-clone"
        CONTAINER_NAME = "netflix-app"
    }

    stages {
        stage('Clone') {
            steps {
                git branch: 'main', url: 'https://github.com/RiyaDesai-2004/Netflix_Deploy.git'
            }
        }

        stage('Validate Files') {
            steps {
                sh 'test -f index.html && test -f style.css && test -f script.js'
                echo 'All critical files present!'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh "docker build -t ${IMAGE_NAME}:latest ."
            }
        }

        stage('Deploy') {
            steps {
                sh "docker stop ${CONTAINER_NAME} || true"
                sh "docker rm ${CONTAINER_NAME} || true"
                sh "docker run -d -p 80:80 --name ${CONTAINER_NAME} ${IMAGE_NAME}:latest"
                echo 'Deployed successfully!'
            }
        }
    }

    post {
        success { echo 'Pipeline succeeded!' }
        failure { echo 'Pipeline failed!' }
    }
}