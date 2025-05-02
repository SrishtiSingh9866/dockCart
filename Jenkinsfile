pipeline {
    agent any

    environment {
        DOCKER_IMAGE = 'dockcart:latest'
    }

    stages {
        stage('Checkout') {
            steps {
                // Clone the repository
                git 'https://github.com/SrishtiSingh9866/dockCart.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                // Build the Docker image using the Dockerfile
                script {
                    docker.build("${DOCKER_IMAGE}")
                }
            }
        }

        stage('Run Tests') {
            steps {
                // Run tests inside the Docker container
                script {
                    docker.image("${DOCKER_IMAGE}").inside {
                        sh 'npm install'
                        sh 'npm test'
                    }
                }
            }
        }

        stage('Deploy') {
            steps {
                // Deploy the application (customize this stage as needed)
                echo 'Deploying the application...'
                // Add deployment steps here
            }
        }
    }

    post {
        always {
            // Clean up Docker images to free up space
            sh 'docker image prune -f'
        }
    }
}
