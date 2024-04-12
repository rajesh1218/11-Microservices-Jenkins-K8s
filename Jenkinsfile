pipeline {
    agent any

    stages {
        stage('Deploy to k8s') {
            steps {
              withKubeCredentials(kubectlCredentials: [[caCertificate: '', clusterName: 'aks-cluster', contextName: '', credentialsId: 'k8-token', namespace: 'webapps', serverUrl: 'aks-cluster-dns-jg6loen3.hcp.eastus.azmk8s.io']]) {
                 sh "kubectl apply -f deployment-service.yml"
                 sleep 80
              }
            }
        }
    }
    stages {
        stage('Verify the deployemnt') {
            steps {
             withKubeCredentials(kubectlCredentials: [[caCertificate: '', clusterName: 'aks-cluster', contextName: '', credentialsId: 'k8-token', namespace: 'webapps', serverUrl: 'aks-cluster-dns-jg6loen3.hcp.eastus.azmk8s.io']]) {
                 sh "kubectl get svc -n webapps"
              }    
            }
        }
    }
}
