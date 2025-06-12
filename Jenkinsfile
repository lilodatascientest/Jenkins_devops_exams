pipeline {
    agent any

    environment {
        KUBECONFIG = '/path/to/kubeconfig' // falls nötig
    }

    stages {
        stage('Deploy to Dev') {
            steps {
                script {
                    sh '''
                    helm upgrade --install cast-db-release ./charts/cast-db \
                      --namespace dev --create-namespace \
                      --values ./charts/cast-db/values-dev.yaml
                    '''
                }
            }
        }

        stage('Deploy to QA') {
            steps {
                script {
                    sh '''
                    helm upgrade --install cast-db-release ./charts/cast-db \
                      --namespace qa --create-namespace \
                      --values ./charts/cast-db/values-qa.yaml
                    '''
                }
            }
        }

        stage('Deploy to Staging') {
            steps {
                script {
                    sh '''
                    helm upgrade --install cast-db-release ./charts/cast-db \
                      --namespace staging --create-namespace \
                      --values ./charts/cast-db/values-staging.yaml
                    '''
                }
            }
        }

        stage('Deploy to Prod') {
            steps {
                script {
                    sh '''
                    helm upgrade --install cast-db-release ./charts/cast-db \
                      --namespace prod --create-namespace \
                      --values ./charts/cast-db/values-prod.yaml
                    '''
                }
            }
        }
    }
}