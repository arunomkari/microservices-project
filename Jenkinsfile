pipeline {
    agent any

    stages {
        stage('Deploy To Kubernetes') {
            steps {
                withKubeCredentials(kubectlCredentials: [[caCertificate: '', clusterName: 'MY-EKS', contextName: '', credentialsId: 'k8-token', namespace: 'https://7A706135F6B100D15CFD11A4C47C1CBF.gr7.ap-south-1.eks.amazonaws.com']]) {
                    sh "kubectl apply -f deployment-service.yml"
                    
                }
            }
        }
        
        stage('verify Deployment') {
            steps {
                withKubeCredentials(kubectlCredentials: [[caCertificate: '', clusterName: 'MY-EKS', contextName: '', credentialsId: 'k8-token', namespace: 'webapps', serverUrl: 'https://7A706135F6B100D15CFD11A4C47C1CBF.gr7.ap-south-1.eks.amazonaws.com']]) {
                    sh "kubectl get svc -n webapps"
                }
            }
        }
    }
}
