pipeline {
    agent any

    environment {
        DOCKER_IMAGE    = "JenkinTest"
        CONTAINER_NAME  = "JenkinTest_container"
    }

    stages {

        stage('Checkout') {
            steps {
                echo 'Checkout source code'
                checkout scm
            }
        }

        stage('Build') {
            steps {
                echo 'Build application'
                sh '''
                echo "Build step here"
                '''
            }
        }

        stage('Test') {
            steps {
                echo 'Run unit tests'
                sh '''
                echo "Run tests here"
                '''
            }
        }

        stage('Build Docker Image') {
            steps {
                echo 'Build Docker image'
                sh """
                docker build -t ${DOCKER_IMAGE}:${DOCKER_TAG} .
                """
            }
        }

        stage('Deploy (Docker Run)') {
            steps {
                echo 'Deploy application using Docker'
                sh """
                docker build -t ${DOCKER_IMAGE} .
                docker run -d --name ${CONTAINER_NAME} ${DOCKER_IMAGE}
                """
            }
        }
    }

    post {
        success {
            echo '✅ Pipeline SUCCESS'
        }
        failure {
            echo '❌ Pipeline FAILED'
        }
        always {
            sh 'docker ps'
        }
    }
}
