pipeline {
    agent any

    environment {
        COMPOSE_CMD = "docker-compose"   // use this if docker-compose not available
        PROJECT_DIR = "mern-tutorial"
    }

    stages {

        stage('Checkout Code') {
            steps {
                checkout scm
            }
        }

        stage('Build Docker Images') {
            steps {
                dir("${PROJECT_DIR}") {
                    sh "${COMPOSE_CMD} build"
                }
            }
        }

        stage('Stop Old Containers') {
            steps {
                dir("${PROJECT_DIR}") {
                    sh "${COMPOSE_CMD} down"
                }
            }
        }

        stage('Start Containers') {
            steps {
                dir("${PROJECT_DIR}") {
                    sh "${COMPOSE_CMD} up -d"
                }
            }
        }

        stage('Remove Unused Images') {
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
