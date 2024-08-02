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
                    sh 'echo "Build id = $BUILD_ID" >> index.html'
                    sh 'docker build -t test-nginx-image .'
                }
            }
        }

        stage('Run Docker Container') {
            steps {
                script {
                    sh 'docker rm -f test-nginx-container && docker run -d -p 8081:80 --name test-nginx-container test-nginx-image'
                }
            }
        }

        stage('Check Docker Container') {
            steps {
                script {
                    sh 'result=$(curl http://localhost:8081 | grep Hello | wc -l)'
                }
            }
        }
    }

    post {
        always {
            script {
                sh 'docker ps'
            }
        }
    }
}
