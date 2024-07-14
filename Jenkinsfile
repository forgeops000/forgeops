pipeline {
    agent any

    environment {
        DOCKER_COMPOSE = '/usr/bin/docker compose'
    }

    stages {
        stage('Checkout') {
            steps {
                script {
                    // Clone repo and checkout the specific branch
                    //git url: 'https://github.com/forgeops000/forgeops.git', branch: 'jenkins-pipeline'
                    git 'https://github.com/forgeops000/forgeops.git'
                }
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
                    // Test
                }
            }
        }
        stage('Deploy') {
            steps {
                script {
                    // Deploy
                    sh "${DOCKER_COMPOSE} -f wordpress/docker-compose.yml up -d"
                }
            }
        }
    }
    post {
        always {
            //sh "${DOCKER_COMPOSE} -f wordpress/docker-compose.yml down"
            script {
                sh "${DOCKER_COMPOSE} -f wordpress/docker-compose.yml up -d"
            }
        }
    }
}