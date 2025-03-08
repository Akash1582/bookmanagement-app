pipeline{
	agent any
	environment {
		DOCKER_IMAGE = "akash1582/bookmanagement-app"
		DOCKER_TAG = "latest"
		DOCKER_CREDENTIALS_ID = "docker-hub-credentials"
   		CONTAINER_NAME = "usermanagementpipeline-usermanagement-application-1"
	}
	stages{
		stage('Run Docker container'){
			steps{
				//Pull the latest image
				sh "docker pull ${DOCKER_IMAGE}:${DOCKER_TAG}"
				
				//Run docker container
				sh "docker run -d --name ${CONTAINER_NAME} -p 8082:8081 ${DOCKER_IMAGE}:${DOCKER_TAG}"

			}
		}
	}
		
	post{
		success{
			echo "Pipeline executed"
		}
		failure{
			echo "Pipeline failed!"
		}
	}
}
