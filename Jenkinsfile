pipeline {
    agent any

    environment {
        REPO_URL = 'https://github.com/your-username/your-repo.git'
        DEPLOY_DIR = '/var/www/html'
    }

    stages {
        stage('Checkout Code') {
            steps {
                script {
                    sh "rm -rf workspace || true"
                    sh "git clone ${REPO_URL} workspace"
                }
            }
        }

        stage('Deploy Files') {
            steps {
                script {
                    sh "sudo cp -r workspace/* ${DEPLOY_DIR}/"
                }
            }
        }

        stage('Restart Apache') {
            steps {
                script {
                    sh "sudo systemctl restart httpd"
                }
            }
        }

        stage('Verify Deployment') {
            steps {
                script {
                    sh "curl -I http://localhost:8001"
                }
            }
        }
    }
}
