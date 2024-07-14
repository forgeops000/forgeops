pipeline {
    agent any

    environment {
        DOCKER_COMPOSE = '/usr/local/bin/docker compose'
    }

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/forgeops000/forgeops.git'
                git checkout jenkins-pipeline
            }
        }
        stage('Build Docker Images') {
            steps {
                script {
                    sh "${DOCKER_COMPOSE} -f wordpress/docker-compose.yml build"
                }
            }
        }
        stage('Run Tests') {
            steps {
                script {
                    sh "${DOCKER_COMPOSE} -f wordpress/docker-compose.yml up -d"
                    // Tu możesz dodać kroki testowania, np. testy jednostkowe lub integracyjne
                }
            }
        }
        stage('Deploy') {
            steps {
                script {
                    // Kroki wdrażania, np. push do rejestru Docker lub wdrożenie na serwerze
                    sh "${DOCKER_COMPOSE} -f wordpress/docker-compose.yml up -d"
                }
            }
        }
    }
    post {
        always {
            script {
                sh "${DOCKER_COMPOSE} -f wordpress/docker-compose.yml up -d"
            }
        }
    }
}