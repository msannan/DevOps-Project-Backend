pipeline {
  agent any
  environment {
		registryCredential = 'dockerhub' 
	}
  stages {
    stage('Build Backend') {
			steps {
				dir('backend-python'){
					sh 'docker build -t sannan1357/backend:$GIT_COMMIT .'
                    sh 'docker container run --rm -p 9090:8080 --name backend -d sannan1357/backend:$GIT_COMMIT' 
				    sh 'sleep 5'
				    sh 'curl -I http://localhost:9090'
				}
			} 
		}
    stage('Publish Image to Dockerhub') {
			steps{
				script {
					docker.withRegistry( '', registryCredential ) {
						sh 'docker push sannan1357/backend:$GIT_COMMIT'
					} 
				}
			} 
		}
	}
}