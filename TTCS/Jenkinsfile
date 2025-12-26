pipeline {
    agent any

    environment {
        DOCKER_IMAGE    = "jenkintest"
        DOCKER_TAG      = "latest"
        CONTAINER_NAME  = "jenkintest_container"
        HOST_PORT       = "8081"
        CONTAINER_PORT  = "80"
    }

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                echo 'Build application (static HTML)'
            }
        }

        stage('Test') {
            steps {
                echo 'No tests for static HTML'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh '''
                docker build -t ${DOCKER_IMAGE}:${DOCKER_TAG} .
                '''
            }
        }

        stage('Deploy Container') {
            steps {
                sh '''
                docker rm -f ${CONTAINER_NAME} || true

                docker run -d \
                  --name ${CONTAINER_NAME} \
                  -p ${HOST_PORT}:${CONTAINER_PORT} \
                  ${DOCKER_IMAGE}:${DOCKER_TAG}
                '''
            }
        }
    }

    post {
        always {
            echo 'Running containers:'
            sh 'docker ps'
        }
    }
}
