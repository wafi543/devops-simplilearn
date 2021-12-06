pipeline {
    agent {
        docker { image 'node:14-alpine' }
    }
    stages {
        stage('Test') {
            steps {
                sh 'ls'
                sh 'python3 --version'
                sh 'node --version'
            }
        }
    }
}