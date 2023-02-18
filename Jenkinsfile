pipeline {
    agent any

    environment {
        dockerImage = ''
    }

    stages {
        
        stage('Build image') {
            steps {
                script {
                    dockerImage = docker.build("phayao/my-app")
                }
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

