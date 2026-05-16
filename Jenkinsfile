pipeline {
agent any


stages {

    stage('Clone Code') {
        steps {
            git branch: 'main',
            url: 'https://github.com/Nalin-web/mern-devops-project.git'
        }
    }

    stage('Build Backend Image') {
        steps {
            sh 'docker build -t ems-backend ./backend'
        }
    }

    stage('Build Frontend Image') {
        steps {
            sh 'docker build -t ems-frontend ./frontend'
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

