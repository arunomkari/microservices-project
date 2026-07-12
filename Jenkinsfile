pipeline {
    agent any

    stages {
        stage('Deploy To Kubernetes') {
            steps {
                withKubeCredentials(kubectlCredentials: [[caCertificate: '', clusterName: 'MY-EKS', contextName: '', credentialsId: 'k8-token', namespace: 'https://57A5A2795DE7ED6F5BAF4FD4D4C7A3A8.gr7.ap-south-1.eks.amazonaws.com']]) {
                    sh "kubectl apply -f deployment-service.yml"
                    
                }
            }
        }
        
        stage('verify Deployment') {
            steps {
                withKubeCredentials(kubectlCredentials: [[caCertificate: '', clusterName: 'MY-EKS', contextName: '', credentialsId: 'k8-token', namespace: 'webapps', serverUrl: 'https://57A5A2795DE7ED6F5BAF4FD4D4C7A3A8.gr7.ap-south-1.eks.amazonaws.com']]) {
                    sh "kubectl get svc -n webapps"
                }
            }
        }
    }
}
