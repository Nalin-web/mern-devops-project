pipeline {
agent any


stages {

    stage('Check Files') {
        steps {
            sh 'pwd'
            sh 'ls -la'
            sh 'find . -maxdepth 3'
        }
    }

    stage('Build Backend Image') {
        steps {
            sh 'docker build -t ems-backend ./backend'
        }
    }
}


}

