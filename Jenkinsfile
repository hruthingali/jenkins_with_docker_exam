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
 
        stage('Run Tests on Docker Image') {
            steps {
                script {
                    // Run tests with unittest discover, targeting test.py
                    sh 'docker run --rm -w /app $DOCKER_IMAGE python -m unittest discover -s /app -p "test.py"'
                }
            }
        }
 
        // Optionally add more stages for deployment, notification, etc.
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
