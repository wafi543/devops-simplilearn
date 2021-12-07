pipeline {
    environment { 
        registry = "wafi543/simplilearn" 
        registryCredential = 'dockerhub_id' 
        dockerImage = ''
    }
    agent any
    stages {
        stage('Test') {
            steps {
                sh 'ls'
                sh 'python3 --version'
                sh 'node --version'
            }
        }
        stage('Building docker image') {
            steps {
                script {
                    dockerImage = docker.build registry + ":$BUILD_NUMBER"
                }
            }
        }
        stage('Push image to Dockerhub') {
            steps {
                script {
                    docker.withRegistry( '', registryCredential ) {
                        dockerImage.push()
                    }
                }
            }
        }
        stage('Cleaning up') {
            steps {
                sh "docker rmi $registry:$BUILD_NUMBER"
            }
        } 
    }
}