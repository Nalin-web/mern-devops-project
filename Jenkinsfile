pipeline {
agent any


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

    stage('Deploy Containers') {
        steps {
            sh 'docker compose down'
            sh 'docker compose up -d'
        }
    }

    stage('Verify Deployment') {
        steps {
            sh 'docker ps'
        }
    }
}


}


