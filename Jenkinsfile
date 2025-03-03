pipeline {
    agent any

    environment {
        REPO_URL = 'https://github.com/SlavaSotnikov/s3-static-task.git'
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
                    sh "sudo rm -rf ${DEPLOY_DIR}/*"
					sh "sudo cp -r workspace/* ${DEPLOY_DIR}/"
					sh "sudo chown -R apache:apache ${DEPLOY_DIR}"
					sh "sudo chmod -R 755 ${DEPLOY_DIR}"
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
