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
		sh 'cp -r frontend/build/asset-manifest.json frontend/build/index.html frontend/build/static /var/www/html/'
            }
        }
        stage('Build Backend') {
	    steps {
		sh '''
      		cd backend
		python3 -m venv venv
  		source venv/bin/activate
        	pip install -r requirements.txt
        	'''
    	    }
	}
        stage('Restart Backend') {
            steps {
                sh 'sudo systemctl restart flask-api'
            }
        }
    }
}
