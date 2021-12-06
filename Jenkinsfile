pipeline {
    agent any {
        agent { dockerfile true }
    }
    stages {
        stage('Test') {
            steps {
                sh 'ls'
                sh 'python3 --version'
            }
        }
    }
}