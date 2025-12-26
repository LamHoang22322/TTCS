pipeline {
    agent any

    environment {
        DOCKER_IMAGE    = "jenkintest"
        DOCKER_TAG     = "latest"
        CONTAINER_NAME  = "jenkintest_container"
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
                sh '''
                docker build -t ${DOCKER_IMAGE}:${DOCKER_TAG} .
                '''
            }
        }

        stage('Deploy Container') {
            steps {
                sh '''
                docker rm -f ${CONTAINER_NAME} || true
                docker run -d --name ${CONTAINER_NAME} ${DOCKER_IMAGE}:${DOCKER_TAG}
                '''
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
