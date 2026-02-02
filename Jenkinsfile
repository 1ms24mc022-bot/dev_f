pipeline {
	agent any
	environment {
		DOCKERHUB_CRED=credentials('dockerhubID')
		IMAGE_NAME="chethan2310/dev_f"
	}
	
	stages {
		stage('checkout') {
			steps {
				git url:'https://github.com/1ms24mc022-bot/dev_f', branch:'main' 
			}
		}
		
		stage('Build Docker Image') {
			steps {
				script {
					dockerImage=docker.build("${IMAGE_NAME}:latest")
				}
			}
		}
		
		stage('Push to DockerHub') {
			steps {
				script {
					docker.withRegistry('https://index.docker.io/v1/','dockerhub') {
						dockerImage.push()
					}
				}
			}
		}
	}
	
	post {
		success {
			echo "Pipeline Successful"
		}
		failure {
			echo "Pipeline Failed"
		}
		always {
			echo "Cleaning Up WorkSpace"
			deleteDir()
		}
	}
}
