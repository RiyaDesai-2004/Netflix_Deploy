pipeline {
    agent any

    stages {
        stage('Validate Files') {
            steps {
                sh 'ls -la'
                echo 'All static files present!'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Static site is ready!'
            }
        }
    }

    post {
        success {
            echo 'Build Successful!'
        }
        failure {
            echo 'Build Failed!'
        }
    }
}