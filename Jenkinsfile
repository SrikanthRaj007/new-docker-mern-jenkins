pipeline {
    agent any

    stages {

        stage('Build Docker Images') {
            steps {
                dir("mern-tutorial") {
                    sh "docker-compose build"
                }
            }
        }

        stage('Stop Old Containers') {
            steps {
                dir("mern-tutorial") {
                    sh "docker-compose down"
                }
            }
        }

        stage('Start Containers') {
            steps {
                dir("mern-tutorial") {
                    sh "docker-compose up -d"
                }
            }
        }
    }

    post {
        success {
            echo 'Deployment Successful 🚀'
        }
        failure {
            echo 'Deployment Failed ❌'
        }
    }
}
