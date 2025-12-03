pipeline {
    agent any

    environment {
        DOCKERHUB_CREDENTIALS = credentials('moaaz-dockerhub')
    }

    stages {

        stage('Build Docker Images') {
            steps {
                script {
                    sh """
                        echo 'Building APP image...'
                        docker build -t moaazfarrag/app:latest ./app

                        echo 'Building DATABASE image...'
                        docker build -t moaazfarrag/database:latest ./database

                        echo 'Building NGINX image...'
                        docker build -t moaazfarrag/nginx:latest ./nginx
                    """
                }
            }
        }

        stage('Login to DockerHub') {
            steps {
                sh """
                echo ${DOCKERHUB_CREDENTIALS_PSW} | docker login \
                    -u ${DOCKERHUB_CREDENTIALS_USR} --password-stdin
                """
            }
        }

        stage('Push Docker Images') {
            steps {
                sh """
                    docker push moaazfarrag/app:latest
                    docker push moaazfarrag/database:latest
                    docker push moaazfarrag/nginx:latest
                """
            }
        }
    }

    post {
        always {
            sh "docker logout"
        }
    }
}
