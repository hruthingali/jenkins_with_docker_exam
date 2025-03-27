pipeline {
    agent any

    environment {
        DOCKER_IMAGE = 'barathkumar29/my-flask-app:latest'  
        ARTIFACT_DIR = 'build'  
    }

    stages {
        stage('Checkout Code') {
            steps {
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
                    sh 'docker run --rm $DOCKER_IMAGE ls -l /app'

                    sh 'docker run --rm $DOCKER_IMAGE pwd'
                }
            }
        }

        stage('Run Tests on Docker Image') {
            steps {
                script {
                    sh 'docker run --rm -w /app $DOCKER_IMAGE python -m unittest discover -s /app -p "test.py"'
                }
            }
        }

        stage('Build Artifacts') {
            steps {
                script {
                    sh 'python setup.py bdist_wheel'

                    sh 'mkdir -p $ARTIFACT_DIR'
                    sh 'cp dist/*.whl $ARTIFACT_DIR/'
                }
            }
        }

        stage('Archive Artifacts') {
            steps {
                archiveArtifacts artifacts: "$ARTIFACT_DIR/*.whl", allowEmptyArchive: true
            }
        }
    }

    post {
        always {
            sh 'docker logout'
        }

        success {
            echo 'Tests passed and artifacts archived successfully!'
        }

        failure {
            echo 'Tests failed. Check the logs for more details.'
        }
    }
}
