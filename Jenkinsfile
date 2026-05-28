pipeline {
    agent any

    tools {
        jdk 'JDK17'
        maven 'Maven'
    }

    stages {

        stage('Clone Repository') {
            steps {
                git branch: 'master',
                url: 'https://github.com/Chethangowda97/onlinebookstore.git'
            }
        }

        stage('Build JAR') {
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
            echo 'JAR file created successfully inside target directory'
        }

        failure {
            echo 'Build failed'
        }
    }
}                -p 80:8080 \
                chethan97/onlinebookstore
                '''
            }
        }
    }
}
