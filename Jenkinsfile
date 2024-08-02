pipeline {
    agent any

    stages {
        stage('Clone Repository') {
            steps {
                git 'https://github.com/nikvladimirovich2/test_hello_world'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    sh 'docker build -t test-nginx-image .'
                }
            }
        }

        stage('Run Docker Container') {
            steps {
                script {
                    sh 'docker run -d -p 8081:80 --name test-nginx-container test-nginx-image'
                }
            }
        }

        stage('Check Docker Container') {
            steps {
                script {
                    sh 'echo "Build id = $BUILD_ID"'
                    sh 'result=$(curl http://localhost:8081 | grep Hello | wc -l)'
                }
            }
        }
    }

    post {
        always {
            script {
                sh 'docker stop test-nginx-container || true'
                sh 'docker rm test-nginx-container || true'
            }
        }
    }
}
