pipeline {
    agent {
        docker {
            image 'docker:latest'
            args '-v /var/run/docker.sock:/var/run/docker.sock'
        }
    }
    environment {
        KUBECONFIG = credentials('kubeconfig-id')  // Replace 'kubeconfig-id' with your Jenkins credential ID
    }
    stages {
        stage('Checkout') {
            steps {
                // Checkout the source code
                checkout scm
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                    // Build the Docker image
                    def image = docker.build("my-docker-image:latest")
                }
            }
        }
        stage('Push Docker Image') {
            steps {
                script {
                    docker.withRegistry('https://index.docker.io/v1/', 'dockerhub-credentials-id') {  // Replace with your Docker Hub credentials ID
                        def image = docker.build("my-docker-image:latest")
                        image.push()
                    }
                }
            }
        }
        stage('Deploy to Kubernetes') {
            steps {
                script {
                    withKubeConfig([credentialsId: 'kubeconfig-id']) {  // Replace 'kubeconfig-id' with your Jenkins credential ID
                        sh 'kubectl apply -f deployment.yaml'
                    }
                }
            }
        }
    }
}
