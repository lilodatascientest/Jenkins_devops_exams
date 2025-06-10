pipeline {
    agent any
  
    environment {
      DOCKERHUB_CREDENTIALS = 'dockerhub-creds' // ID from Jenkins credentials
      DOCKERHUB_REPO = 'lilodin/myapp'
      IMAGE_TAG = "${env.BUILD_NUMBER}"
    }

    stages {
        stage('Checkout Code') {
          steps {
            git 'https://github.com/lilodatascientest/Jenkins_devops_exams.git'
            echo "${DOCKERHUB_CREDENTIALS}"
            echo "${DOCKERHUB_REPO}"
            echo "${IMAGE_TAG}"
            }
        }

        stage('Build Docker Image') {
          steps {
            script {
                def image = docker.build("${DOCKERHUB_REPO}:${IMAGE_TAG}", "-f cast-service/Dockerfile cast-service")
            }
          }            
        }


        stage('Push to DockerHub') {
          steps {
            script {
              docker.withRegistry('https://index.docker.io/v1/', DOCKERHUB_CREDENTIALS) {
                docker.image("${DOCKERHUB_REPO}:${IMAGE_TAG}").push()
              }
            }
          }
        }

    } 
}
