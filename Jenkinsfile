pipeline {
    agent any

    environment {
        AWS_DEFAULT_REGION = 'ap-south-1'
        CLUSTER_NAME = 'MY-EKS'
    }

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Configure EKS') {
            steps {
                sh '''
                    aws eks update-kubeconfig \
                      --region $AWS_DEFAULT_REGION \
                      --name $CLUSTER_NAME

                    kubectl get nodes
                '''
            }
        }

        stage('Deploy To Kubernetes') {
            steps {
                sh '''
                    kubectl apply -f deployment-service.yml -n webapps
                '''
            }
        }

        stage('Verify Deployment') {
            steps {
                sh '''
                    kubectl get deployment -n webapps
                    kubectl get pods -n webapps
                    kubectl get svc -n webapps
                '''
            }
        }
    }

    post {
        always {
            echo 'Pipeline Execution Completed'
        }

        success {
            echo 'Deployment Successful'
        }

        failure {
            echo 'Deployment Failed'
        }
    }
}
