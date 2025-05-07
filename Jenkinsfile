pipeline {
    agent any
    stages {
        stage('Check Docker Daemon Access') {
            steps {
                sh 'docker ps'
            }
        }
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/Sangam200/flask-starter'
            }
        }
        stage('Build Docker Image') {
            steps {
                sh 'docker build -t flask-student .'
            }
        }
        stage('Stop Previous Container') {
            steps {
                script {
                    sh 'docker ps -q --filter "name=flask-student-container" | xargs -r docker stop || true'
                    sh 'docker ps -a -q --filter "name=flask-student-container" | xargs -r docker rm || true'
                }
            }
        }
        stage('Run New Docker Container') {
            steps {
                sh 'docker run -d -p 5000:5000 --name flask-student-container flask-student'
            }
        }
    }
    post {
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed!'
        }
    }
}
