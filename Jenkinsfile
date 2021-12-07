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
                catchError {
                    sh "docker rm -f devops"
                }
                sh "docker run -d --name devops --restart always $registry:$BUILD_NUMBER"
            }
        } 
    }
}