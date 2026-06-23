pipeline {
    agent any
 
    stages {
        stage('Checkout') {
            steps {
                echo 'Checking out code from GitHub'
            }
        }
        stage('Build') {
            steps {
                echo 'Building the application'
            }
        }
        stage('Test') {
            steps {
                echo 'Running tests'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying application'
            }
        }
        stage('Docker Build') {
            steps {
                sh 'docker build -t cicd-demo:latest .'
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
