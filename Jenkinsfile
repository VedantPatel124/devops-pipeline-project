pipeline {
    agent any
    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main', url: 'https://github.com/VedantPatel124/devops-pipeline-project.git'
            }
        }
        stage('Build Frontend') {
            steps {
		dir('frontend') {  // Navigate to the frontend directory
            		sh 'export NODE_OPTIONS=--openssl-legacy-provider && npm install && npm run build'
		}
            }
        }
        stage('Deploy Frontend') {
            steps {
                sh 'sudo cp -r frontend/build/* /var/www/html/'
            }
        }
        stage('Build Backend') {
            steps {
                sh 'cd backend && pip3 install -r requirements.txt'
            }
        }
        stage('Restart Backend') {
            steps {
                sh 'sudo systemctl restart flask-api'
            }
        }
    }
}
