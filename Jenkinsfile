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
    } 
}
