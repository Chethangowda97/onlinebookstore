pipeline {
    agent any

    environment {
        DOCKER_IMAGE = "chethan97/onlinebookstore"
    }

    stages {

        stage('Clone Code') {
            steps {
                git 'https://github.com/Chethangowda97/onlinebookstore.git'
            }
        }

        stage('Build Application') {
            steps {
                sh 'chmod +x mvnw'
                sh './mvnw clean package -DskipTests'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $DOCKER_IMAGE .'
            }
        }

        stage('Docker Login') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'dockerhub',
                    usernameVariable: 'DOCKER_USER',
                    passwordVariable: 'DOCKER_PASS'
                )]) {

                    sh 'echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin'
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                sh 'docker push $DOCKER_IMAGE'
            }
        }

        stage('Deploy Container') {
            steps {
                sh '''
                docker stop onlinebookstore || true
                docker rm onlinebookstore || true

                docker run -d \
                --name onlinebookstore \
                -p 80:8080 \
                $DOCKER_IMAGE
                '''
            }
        }
    }
}
