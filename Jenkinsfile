pipeline {
    agent any

    environment {
        DOCKER_COMPOSE = "docker-compose"
        PROJECT_NAME = "mern-tutorial"
    }

    stages {

        stage('Clean Workspace') {
            steps {
                cleanWs()
            }
        }

        stage('Clone Repository') {
            steps {
                git branch: 'main', 
                    url: 'https://github.com/SrikanthRaj007/docker-jenkins-mern.git'
            }
        }

        stage('Build Docker Images') {
            steps {
                sh "${DOCKER_COMPOSE} build"
            }
        }

        stage('Stop Old Containers') {
            steps {
                sh "${DOCKER_COMPOSE} down"
            }
        }

        stage('Start Containers') {
            steps {
                sh "${DOCKER_COMPOSE} up -d"
            }
        }

        stage('Remove Unused Docker Images') {
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
