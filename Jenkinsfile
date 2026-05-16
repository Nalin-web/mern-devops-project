pipeline {
agent any

environment {
    AWS_ACCOUNT_ID = "ACCOUNT-ID"
    AWS_REGION = "ap-south-1"
    BACKEND_REPO = "ems-backend"
    FRONTEND_REPO = "ems-frontend"
}

stages {

    stage('Build Backend Image') {
        steps {
            sh 'docker build -t ems-backend ./server'
        }
    }

    stage('Build Frontend Image') {
        steps {
            sh 'docker build -t ems-frontend ./client'
        }
    }

    stage('Login to ECR') {
        steps {
            sh '''
            aws ecr get-login-password --region $AWS_REGION | docker login --username AWS --password-stdin $AWS_ACCOUNT_ID.dkr.ecr.$AWS_REGION.amazonaws.com
            '''
        }
    }

    stage('Tag Backend Image') {
        steps {
            sh '''
            docker tag ems-backend:latest $AWS_ACCOUNT_ID.dkr.ecr.$AWS_REGION.amazonaws.com/$BACKEND_REPO:latest
            '''
        }
    }

    stage('Tag Frontend Image') {
        steps {
            sh '''
            docker tag ems-frontend:latest $AWS_ACCOUNT_ID.dkr.ecr.$AWS_REGION.amazonaws.com/$FRONTEND_REPO:latest
            '''
        }
    }

    stage('Push Backend Image') {
        steps {
            sh '''
            docker push $AWS_ACCOUNT_ID.dkr.ecr.$AWS_REGION.amazonaws.com/$BACKEND_REPO:latest
            '''
        }
    }

    stage('Push Frontend Image') {
        steps {
            sh '''
            docker push $AWS_ACCOUNT_ID.dkr.ecr.$AWS_REGION.amazonaws.com/$FRONTEND_REPO:latest
            '''
        }
    }

    stage('Deploy Containers') {
        steps {
            sh '/usr/local/bin/docker-compose down'
            sh '/usr/local/bin/docker-compose up -d'
        }
    }

    stage('Verify Deployment') {
        steps {
            sh 'docker ps'
        }
    }
}

}

