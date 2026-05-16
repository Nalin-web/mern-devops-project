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
            sh '/usr/bin/docker compose down'
            sh '/usr.bin/docker-compose up -d'
        }
    }

    stage('Verify Deployment') {
        steps {
            sh 'docker ps'
        }
    }
}


}


