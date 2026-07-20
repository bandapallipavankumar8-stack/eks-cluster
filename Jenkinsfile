pipeline {
    agent any
    environment {
        AWS_REGION     = 'ap-south-1' 
        CLUSTER_NAME   = 'your-mumbai-eks-cluster'
    }
    stages {
        stage('Authenticate & Connect') {
            // This safely injects the keys into the shell environment
            withCredentials([
                string(credentialsId: 'AWS_ACCESS_KEY_ID', variable: 'AWS_ACCESS_KEY_ID'),
                string(credentialsId: 'AWS_SECRET_ACCESS_KEY', variable: 'AWS_SECRET_ACCESS_KEY')
            ]) {
                steps {
                    sh '''
                        aws eks update-kubeconfig --region ${AWS_REGION} --name ${CLUSTER_NAME}
                        kubectl cluster-info
                        kubectl get nodes
                    '''
                }
            }
        }
        stage('Deploy to Mumbai EKS') {
            steps {
                sh '''
                    kubectl apply -f deployment.yaml
                '''
            }
        }
    }
}
