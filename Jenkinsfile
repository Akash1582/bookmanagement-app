pipeline{
	agent any
	environment {
		DOCKER_IMAGE = "akash1582/bookmanagement-app"
		DOCKER_TAG = "latest"
		DOCKER_CREDENTIALS_ID = "bhesalakash123@gmail.com"
		GITHUB_REPO = "https://github.com/Akash1582/bookmanagement-app.git"

	}
	Stages{
		stage('Clone Repo'){
			steps{
				git branch: 'master', url: "${GITHUB_REPO}"
			}
		}
		stage('Build Maven Project'){
			steps{
				sh 'mvn clean package'
			}
		}
		stage('Build Docker Image'){
			steps{
				sh "docker build -t ${DOCKER_IMAGE}":${DOCKER_TAG} ."
			}
		}
		stage('Push to Docker Hub'){
			steps{
				withCredentials([usernamePassword(credentialsId: "${DOCKER_CREDENTAILS_IT}", usernameVariable: "DOCKER_USER", passwordVariable: "DOCKER_PASS")]){
					sh "echo ${DOCKER_PASS} | docker login -u ${DOCKER_USER} ==password-stdin"
					sh "docker push ${DOCKER_IMAGE}:${DOCKER_TAG}"
				}
			}
		}
		stage('Deploy to minikube'){
			steps{
				sh 'minikube start'
				sh 'kubectl apply -f kubernetes.yaml'
				sh 'kubectl get pods'
			}
		}
	}
	post{
		success{
			echo "Pipeline successfull"
		}
		failure{
			echo "Pipeline failed"
		}
	}
}
