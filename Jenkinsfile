pipeline {
    agent any

    stages {

        stage('Clone Repository') {
            steps {
                git branch: 'master',
                url: 'https://github.com/Chethangowda97/onlinebookstore.git'
            }
        }

        stage('Check Java & Maven') {
            steps {
                sh 'java -version'
                sh 'mvn -version'
            }
        }

        stage('Build JAR/WAR') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Verify Target Folder') {
            steps {
                sh 'ls -la target'
            }
        }
    }

    post {
        success {
            echo 'Build completed successfully'
        }

        failure {
            echo 'Build failed'
        }
    }
}
