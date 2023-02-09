pipeline {
    agent any
    
    environment {
		DOCKERHUB_CREDENTIALS=credentials('DockerHub')
	}
	
    stages {
        stage('GitCheckout') {
            steps {
                git branch: 'main', url: 'https://github.com/akshaydevops97/node-todo-app.git'
            }
        }
        stage('DockerBuild') {
            steps {
                sh 'docker build -t akshaydevops97/todoapp:latest .'
            }
        }
        stage('Login') {

			steps {
				sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
			}
		}

		stage('Push') {

			steps {
				sh 'docker push akshaydevops97/todoapp:latest'
			}
		}
		stage('Deploy') {

			steps {
				//sh 'docker-compose down && docker-compose up -d -f docker-compose.yaml'
				//sh 'docker run --name node-app -d -p 8000:8000 akshaydevops97/node-app:latest'
				sh 'kubectl create -f deployment.yaml'
				
			}
		}
    }
}
