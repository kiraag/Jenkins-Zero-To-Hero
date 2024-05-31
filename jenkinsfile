pipeline {
    agent any

    environment {
        SONARQUBE_IMAGE = 'sonarqube:latest'
        CONTAINER_NAME = 'sonarqube-container'
    }

    stages {
        stage('Pull SonarQube Docker Image') {
            steps {
                script {
                    echo "Pulling SonarQube Docker image..."
                    sh "docker pull ${env.SONARQUBE_IMAGE}"
                }
            }
        }

        stage('Run SonarQube Container') {
            steps {
                script {
                    echo "Running SonarQube container..."
                    sh "docker run -d --name ${env.CONTAINER_NAME} -p 9000:9000 ${env.SONARQUBE_IMAGE}"
                    
                    // Wait for SonarQube to be fully started
                    echo "Waiting for SonarQube to start..."
                    sleep 60 // Adjust sleep time if necessary
                }
            }
        }

        stage('Check SonarQube Version') {
            steps {
                script {
                    echo "Checking SonarQube version..."
                    // Here we exec into the container to get the version
                    sh "docker exec ${env.CONTAINER_NAME} sonarqube --version"
                }
            }
        }
    }

    post {
        always {
            script {
                echo "Cleaning up..."
                // Stop and remove the SonarQube container
                sh "docker stop ${env.CONTAINER_NAME}"
                sh "docker rm ${env.CONTAINER_NAME}"
            }
        }
    }
}
