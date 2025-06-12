pipeline {
    agent any

    stages {
        stage('Deploy to Dev') {
            steps {
                withCredentials([file(credentialsId: 'kubeconfig-dev', variable: 'KUBECONFIG_FILE')]) {
                    sh '''
                    export KUBECONFIG=$KUBECONFIG_FILE
                    helm upgrade --install cast-db-release ./charts/cast-db \
                      --namespace dev --create-namespace \
                      --values ./charts/cast-db/values-dev.yaml
                    '''
                }
            }
        }

        stage('Deploy to QA') {
            steps {
                withCredentials([file(credentialsId: 'kubeconfig-dev', variable: 'KUBECONFIG_FILE')]) {
                    sh '''
                    export KUBECONFIG=$KUBECONFIG_FILE
                    helm upgrade --install cast-db-release ./charts/cast-db \
                      --namespace qa --create-namespace \
                      --values ./charts/cast-db/values-qa.yaml
                    '''
                }
            }
        }

        stage('Deploy to Staging') {
            steps {
                withCredentials([file(credentialsId: 'kubeconfig-dev', variable: 'KUBECONFIG_FILE')]) {
                    sh '''
                    export KUBECONFIG=$KUBECONFIG_FILE
                    helm upgrade --install cast-db-release ./charts/cast-db \
                      --namespace staging --create-namespace \
                      --values ./charts/cast-db/values-staging.yaml
                    '''
                }
            }
        }

        stage('Deploy to Prod') {
            steps {
                withCredentials([file(credentialsId: 'kubeconfig-dev', variable: 'KUBECONFIG_FILE')]) {
                    sh '''
                    export KUBECONFIG=$KUBECONFIG_FILE
                    helm upgrade --install cast-db-release ./charts/cast-db \
                      --namespace prod --create-namespace \
                      --values ./charts/cast-db/values-prod.yaml
                    '''
                }
            }
        }
    }
}
