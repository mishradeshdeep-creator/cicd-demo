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
    stage('Database Migration') {
    steps {
        sh '''
            liquibase \
            --url=jdbc:postgresql://cicd-demo-db.c3aq80qsa382.ap-south-1.rds.amazonaws.com:5432/appdb \
            --username=CotrollerDB \
            --password=Admin12345! \
            --changeLogFile=db/changelog/db.changelog-root.xml \
            --classpath=/usr/local/liquibase/lib/postgresql-42.6.0.jar \
            update
        '''
    }
}
        stage('Docker Build & Push to ECR') {
        steps {
           sh 'aws ecr get-login-password --region ap-south-1 > /tmp/pass.txt'
           sh 'docker login --username AWS --password-stdin 430689518036.dkr.ecr.ap-south-1.amazonaws.com < /tmp/pass.txt'
           sh 'docker build -t cicd-demo:latest .'
           sh 'docker tag cicd-demo:latest 430689518036.dkr.ecr.ap-south-1.amazonaws.com/cicd-demo:latest'
           sh 'docker push 430689518036.dkr.ecr.ap-south-1.amazonaws.com/cicd-demo:latest'
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