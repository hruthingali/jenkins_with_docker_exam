pipeline {
    agent any
 
    environment {
        DOCKER_IMAGE = 'hruthingali/my-flask-app25:latest'  // Docker image on Docker Hub
    }
 
    stages {
        stage('Checkout Code') {
            steps {
                // Checkout the latest code from your GitHub repository
                git url: 'https://github.com/hruthingali/jenkins_with_docker_exam.git', branch: 'main'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    sh 'docker build -t $DOCKER_IMAGE .'
                }
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
                    sh 'docker run --rm -w /app $DOCKER_IMAGE python -m unittest discover -s /app -p "test.py" > test_results.log'
                }
            }
        }

        stage('Archive Test Results') {
            steps {
                archiveArtifacts artifacts: 'test_results.log', fingerprint: true
            }
        }
    }
 
    post {
        
 
        success {
            echo 'Tests passed successfully!'
        }
 
        failure {
            echo 'Tests failed. Check the logs for more details.'
        }
    }
}
