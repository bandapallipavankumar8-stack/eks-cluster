pipeline {
    agent any
    environment {
        // Explicitly target the Mumbai region
        AWS_REGION     = 'ap-south-1' 
        CLUSTER_NAME   = 'your-mumbai-eks-cluster'
    }
    stages {
        stage('Authenticate & Connect') {
            steps {
                sh '''
                    # 1. Force the AWS CLI to look in Mumbai
                    aws eks update-kubeconfig --region ${AWS_REGION} --name ${CLUSTER_NAME}
                    
                    # 2. Test the connection
                    kubectl cluster-info
                    kubectl get nodes
                '''
            }
        }
        stage('Deploy to Mumbai EKS') {
            steps {
                sh '''
                    # Apply your kubernetes deployment files
                    kubectl apply -f deployment.yaml
                '''
            }
        }
    }
}
