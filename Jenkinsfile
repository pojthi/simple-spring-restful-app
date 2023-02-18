pipeline {
    agent any

    environment {
        dockerImage = ''
    }

    stages {
        
        stage('Build image') {
            steps {
                sh 'docker build -t pojthi/simple-spring-restful-app:latest .'
            }
        }
        stage('Push image') {
            steps {
                script {
                    withDockerRegistry(
                        credentialsId: 'docker-credential',
                        url: 'https://10.247.24.15:8443') {
                        dockerImage.push()
                    }
                }
            }
        }
        stage('Deployment') {
            steps {
                sh 'kubectl apply -f deployment.yml';
            }
        }
    }
}

