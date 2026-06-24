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
        stage('Docker Build & Push to ECR') {
            steps {
                 sh '''
                    aws ecr get-login-password --region ap-south-1 | docker login --username AWS --password-stdin 430689518036.dkr.ecr.ap-south-1.amazonaws.com
                    docker build -t cicd-demo:latest .
                    docker tag cicd-demo:latest 430689518036.dkr.ecr.ap-south-1.amazonaws.com/cicd-demo:latest
                    docker push 430689518036.dkr.ecr.ap-south-1.amazonaws.com/cicd-demo:latest
             '''
            }
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
