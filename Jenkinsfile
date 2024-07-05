pipeline {
    agent any
    stages {
        stage('Clone Repository') {
            steps {
                git ' https://github.com/Kumarazdevops/Project-work1.git'
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                    dockerImage = docker.build("app:${env.BUILD_ID}")
                }
            }
        }
        stage('Test') {
            steps {
                script {
                    dockerImage.inside {
                        sh 'run-tests.sh'
                    }
                }
            }
        }
        stage('Deploy') {
            steps {
                script {
                    dockerImage.push('app:latest')
                    sh 'docker-compose up -d'
                }
            }
        }
    }
}
 
