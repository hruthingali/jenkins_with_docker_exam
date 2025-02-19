pipeline {
    agent any
 
    environment {
        DOCKER_IMAGE = 'barathkumar29/my-flask-app:latest'  // Docker image on Docker Hub
    }
 
    stages {
        stage('Checkout Code') {
            steps {
                // Checkout the latest code from your GitHub repository
                git url: 'https://github.com/jkbarathkumar/jenkins_with_docker', branch: 'main'
            }
        }
        
        stage('Pull Latest Docker Image') {
            steps {
                script {
                    sh 'docker pull $DOCKER_IMAGE'
                }
            }
        }

        stage('Debug Docker Container') {
            steps {
                script {
                    // Check if test.py exists in the container
                    sh 'docker run --rm $DOCKER_IMAGE ls -l /app'
                    
                    // Print working directory inside container
                    sh 'docker run --rm $DOCKER_IMAGE pwd'
                }
            }
        }

        stage('Run Tests on Docker Image') {
            steps {
                script {
                    // Run tests with unittest discover, targeting test.py
                    sh 'docker run --rm -w /app $DOCKER_IMAGE python -m unittest discover -s /app -p "test.py"'
                }
            }
        }
    }
 
    post {
        always {
            // Clean up: Logout from Docker registry after the build (optional for public images)
            sh 'docker logout'
        }
 
        success {
            echo 'Tests passed successfully!'
        }
 
        failure {
            echo 'Tests failed. Check the logs for more details.'
        }
    }
}
