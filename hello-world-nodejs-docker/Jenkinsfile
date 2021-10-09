pipeline {
  agent any
  environment {
		registryCredential = 'dockerhub' 
	}
  stages {
    stage('Build') {
			steps {
				dir('hello-world-nodejs-docker'){
					sh 'docker build -t kahootali/test-node-app .'
				}
			} 
		}
    stage('Test') {
      steps {
			dir('hello-world-nodejs-docker'){
				sh 'docker container run --rm -p 8001:8080 --name node -d kahootali/test-node-app' 
				sh 'sleep 5'
				sh 'curl -I http://localhost:8001'
			}
		} 
	}
    stage('Publish') {
			steps{
				script {
					docker.withRegistry( '', registryCredential ) {
						sh 'docker push kahootali/test-node-app:latest'
					} 
				}
			} 
		}
	}
}