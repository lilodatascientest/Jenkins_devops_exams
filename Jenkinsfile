pipeline {
    agent any

    stages {
        stage('Deploy to Dev') {
            steps {
                withCredentials([file(credentialsId: 'kubeconfig-dev', variable: 'KUBECONFIG_FILE')]) {
                    sh '''
                    export KUBECONFIG=$KUBECONFIG_FILE
                    helm upgrade --install cast-db-release ./charts \
                      --namespace dev --create-namespace \
                      --values ./charts/values.yaml
                    '''
                }
            }
        }

        stage('Deploy to QA') {
            steps {
                withCredentials([file(credentialsId: 'kubeconfig-dev', variable: 'KUBECONFIG_FILE')]) {
                    sh '''
                    export KUBECONFIG=$KUBECONFIG_FILE
                    helm upgrade --install cast-db-release ./charts \
                      --namespace qa --create-namespace \
                      --values ./charts/values.yaml
                    '''
                }
            }
        }

        stage('Deploy to Staging') {
            steps {
                withCredentials([file(credentialsId: 'kubeconfig-dev', variable: 'KUBECONFIG_FILE')]) {
                    sh '''
                    export KUBECONFIG=$KUBECONFIG_FILE
                    helm upgrade --install cast-db-release ./charts \
                      --namespace staging --create-namespace \
                      --values ./charts/values.yaml
                    '''
                }
            }
        }

        stage('Deploy to Prod') {
            steps {
                withCredentials([file(credentialsId: 'kubeconfig-dev', variable: 'KUBECONFIG_FILE')]) {
                    sh '''
                    export KUBECONFIG=$KUBECONFIG_FILE
                    helm upgrade --install cast-db-release ./charts \
                      --namespace prod --create-namespace \
                      --values ./charts/values.yaml
                    '''
                }
            }
        }
    }
}
