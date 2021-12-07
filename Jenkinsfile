pipeline {
    environment { 
        registry = "wafi543/simplilearn" 
        registryCredential = 'dockerhub_id' 
        dockerImage = ''
    }
    agent any
    stages {
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
        stage('Run Container') {
            steps {
                sh "docker run --rm --stop-timeout 5 $registry:$BUILD_NUMBER"
            }
        }
        stage('Cleaning up') {
            steps {
                sh "docker rmi $registry:$BUILD_NUMBER"
            }
        } 
    }
}