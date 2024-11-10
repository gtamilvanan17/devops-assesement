pipeline {
    agent any

    environment {
        DOCKER_IMAGE = 'myapp:latest'  // Replace with your image
        KUBECONFIG_FILE = '/path/to/kubeconfig'  // Path to kubeconfig on Jenkins server
    }

    stages {
        stage('Checkout Code') {
            steps {
                checkout scm
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                script {
                    withKubeConfig([credentialsId: 'kubeconfig-credential-id']) {
                        sh 'kubectl apply -f kubernetes-config.yaml'
                    }
                }
            }
        }

        stage('Post Deployment Verification') {
            steps {
                script {
                    sh 'kubectl get pods -n devops-assesement'
                    sh 'kubectl get hpa -n devops-assesement'
                }
            }
        }
    }

    post {
        success {
            echo 'Deployment succeeded!'
        }
        failure {
            echo 'Deployment failed!'
        }
    }
}
