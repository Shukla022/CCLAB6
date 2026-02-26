pipeline {
    agent any

    stages {

        stage('Checkout SCM') {
            steps {
                echo "Code already checked out by Jenkins"
            }
        }

        stage('Build Backend Image') {
            steps {
                sh 'docker rmi -f backend-app || true'
                sh 'docker build -t backend-app ./backend'
            }
        }

        stage('Deploy Backend Container') {
            steps {
                sh 'docker rm -f backend-container || true'
                sh 'docker run -d --name backend-container -p 8081:8080 backend-app'
            }
        }

        stage('Build NGINX Image') {
            steps {
                sh 'docker rmi -f nginx-app || true'
                sh 'docker build -t nginx-app ./nginx'
            }
        }

        stage('Deploy NGINX Load Balancer') {
            steps {
                sh 'docker rm -f nginx-container || true'
                sh 'docker run -d --name nginx-container -p 80:80 nginx-app'
            }
        }

        stage('Post Actions') {
            steps {
                echo 'Pipeline executed successfully.'
            }
        }
    }
}
