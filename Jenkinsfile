
pipeline {
    agent any

    environment {
        IMAGE_NAME = "jenkins-docker-poc"
    }

    stages {

        stage('Checkout Code') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/kuchipudidora-dot/jenkins-docker-poc.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Run Tests') {
            steps {
                sh 'npm test'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $IMAGE_NAME .'
            }
        }

        stage('Deploy Container') {
            steps {
                sh '''
                  docker rm -f app || true
                  docker run -d -p 3000:3000 --name app $IMAGE_NAME
                '''
            }
        }
    }

    post {
        success {
            echo "✅ Jenkins Docker CI Pipeline Successful"
        }
        failure {
            echo "❌ Jenkins Pipeline Failed"
        }
    }
}
