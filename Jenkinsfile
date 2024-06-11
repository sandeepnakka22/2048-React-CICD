pipeline {
    agent {
        docker {
            image 'docker:latest'
            args '-v /var/run/docker.sock:/var/run/docker.sock -u root'  // Use root user to ensure permissions
        }
    }
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                    def image = docker.build("my-docker-image:latest")
                }
            }
        }
        stage('Run Docker Container') {
            steps {
                script {
                    docker.image("my-docker-image:latest").inside {
                        sh 'echo "Hello from inside the container!"'
                    }
                }
            }
        }
    }
}
