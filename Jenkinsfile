pipeline {
    agent any

    stages {
        stage('Deploy To Kubernetes') {
            steps {
                withKubeCredentials(kubectlCredentials: [[caCertificate: '', clusterName: 'MY-EKS', contextName: '', credentialsId: 'k8-token', namespace: 'https://53C80F7A7E83AFB85E1C8DB618F49010.gr7.ap-south-1.eks.amazonaws.com']]) {
                    sh "kubectl apply -f deployment-service.yml"
                    
                }
            }
        }
        
        stage('verify Deployment') {
            steps {
                withKubeCredentials(kubectlCredentials: [[caCertificate: '', clusterName: 'MY-EKS', contextName: '', credentialsId: 'k8-token', namespace: 'webapps', serverUrl: 'https://53C80F7A7E83AFB85E1C8DB618F49010.gr7.ap-south-1.eks.amazonaws.com']]) {
                    sh "kubectl get svc -n webapps"
                }
            }
        }
    }
}
