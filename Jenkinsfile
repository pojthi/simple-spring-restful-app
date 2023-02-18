pipeline {
    agent any

   
    stages {
        
        stage('Build image') {
            steps {
                sh 'docker build -t simple-spring-restful-app .'
            }
        }
        stage('Push Docker Images to Nexus Registry'){
			sh 'docker login -u npaonline01 -p npaonline01only 10.247.24.15:8443'	
			sh 'docker push 10.247.24.15:8443/simple-spring-restful-app}'
			sh 'docker rmi $(docker images --filter=reference="10.247.24.15:8443/simple-spring-restful-app*" -q)'
			sh 'docker logout 10.247.24.15:8443'
		}
        stage('Deployment') {
            steps {
                sh 'kubectl apply -f deployment.yml';
            }
        }
    }
}

