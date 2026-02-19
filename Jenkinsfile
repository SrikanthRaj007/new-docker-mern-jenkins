pipeline {
    agent any

    environment {
        COMPOSE_CMD = "docker-compose"
        PROJECT_DIR = "mern-tutorial"
    }

    stages {

        stage('Checkout Code') {
            steps {
                checkout scm
            }
        }

        stage('Build & Deploy') {
            steps {
                dir("${PROJECT_DIR}") {
                    sh "${COMPOSE_CMD} down || true"
                    sh "${COMPOSE_CMD} up -d --build"
                }
            }
        }

        stage('Cleanup Images') {
            steps {
                sh "docker image prune -f"
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
