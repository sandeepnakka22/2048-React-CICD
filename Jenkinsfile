pipeline {
    agent {
        docker {
            image 'docker:latest'
            args '-v /var/run/docker.sock:/var/run/docker.sock'
        }
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
        stage('Run Docker Container') {
            steps {
                script {
                    // Run the Docker container
                    docker.image("my-docker-image:latest").inside {
                        sh 'echo "Hello from inside the container!"'
                    }
                }
            }
        }
    }
}
