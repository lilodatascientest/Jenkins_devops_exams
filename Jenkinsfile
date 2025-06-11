pipeline {
    agent any
  
    environment {
      DOCKERHUB_CREDENTIALS = 'dockerhub-creds' // ID from Jenkins credentials
      IMAGE_TAG = 'latest'
    }

    stages {
        stage('Checkout Code') {
          steps {
            git 'https://github.com/lilodatascientest/Jenkins_devops_exams.git'
            echo "${DOCKERHUB_CREDENTIALS}"
            echo "${IMAGE_TAG}"
            }
        }

        stage('Build and Push Cast-Service') {
          steps {
            script {
                def castImage = docker.build("lilodin/cast-service:${IMAGE_TAG}", "-f cast-service/Dockerfile cast-service")
                docker.withRegistry('https://index.docker.io/v1/', DOCKERHUB_CREDENTIALS) {
                    castImage.push()
                }
              }            
            }
          }


        stage('Build and Push Movie-Service') {
          steps {
            script {
                def movieImage = docker.build("lilodin/movie-service:${IMAGE_TAG}", "-f movie-service/Dockerfile movie-service")
                docker.withRegistry('https://index.docker.io/v1/', DOCKERHUB_CREDENTIALS) {
                    movieImage.push()
              }
            }
          }
        }

        stage('Deploy Cast DB to DEV') {
          steps {
            sh 'kubectl apply -f k8s/cast-db-deployment.yaml --namespace=dev'
          }
        }

      stage('Deploy Cast Service to DEV') {
        steps {
          sh 'kubectl apply -f k8s/cast-service-deployment.yaml --namespace=dev'
        }
      }

      stage('Deploy Cast DB to QA') {
        steps {
          sh 'kubectl apply -f k8s/cast-db-deployment.yaml --namespace=qa'
        }
      }

      stage('Deploy Cast Service to QA') {
        steps {
          sh 'kubectl apply -f k8s/cast-service-deployment.yaml --namespace=qa'
        }
      }

      stage('Deploy Cast DB to STAGING') {
        steps {
          sh 'kubectl apply -f k8s/cast-db-deployment.yaml --namespace=staging'
        }
      }

      stage('Deploy Cast Service to STAGING') {
        steps {
          sh 'kubectl apply -f k8s/cast-service-deployment.yaml --namespace=staging'
        }
      }

      stage('Deploy Cast DB to PROD') {
        steps {
          sh 'kubectl apply -f k8s/cast-db-deployment.yaml --namespace=prod'
        }
      }

      stage('Deploy Cast Service to PROD') {
        steps {
          sh 'kubectl apply -f k8s/cast-service-deployment.yaml --namespace=prod'
        }
      }

    } 
}
