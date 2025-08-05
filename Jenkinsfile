pipeline {
    agent any

    environment {
        IMAGE_NAME = "node-docker-ci"
        CONTAINER_NAME = "node-app"
        PORT = "3000"
    }

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/ajaygitj/jen-docker.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    sh "docker build -t $IMAGE_NAME ."
                }
            }
        }

        stage('Stop Previous Container') {
            steps {
                script {
                    sh "docker rm -f $CONTAINER_NAME || true"
                }
            }
        }

        stage('Run New Container') {
            steps {
                script {
                    sh "docker run -d --name $CONTAINER_NAME -p $PORT:$PORT $IMAGE_NAME"
                }
            }
        }
    }

    post {
        success {
            echo '✅ App deployed successfully!'
        }
        failure {
            echo '❌ Deployment failed.'
        }
    }
}
