pipeline {
    agent any
    environment {
        AWS_REGION     = 'ap-south-1' 
        CLUSTER_NAME   = 'your-mumbai-eks-cluster' // Remember to change this to your exact EKS cluster name
    }
    stages {
        stage('Authenticate & Connect') {
            steps {
                // withCredentials belongs inside the steps block
                withCredentials([
                    string(credentialsId: 'AWS_ACCESS_KEY_ID', variable: 'AWS_ACCESS_KEY_ID'),
                    string(credentialsId: 'AWS_SECRET_ACCESS_KEY', variable: 'AWS_SECRET_ACCESS_KEY')
                ]) {
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
                    # Add your deployment commands here, for example:
                    # kubectl apply -f deployment.yaml
                    echo "Authentication successful!"
                '''
            }
        }
    }
}
