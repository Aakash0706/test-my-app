pipeline {
    agent any
    triggers{
        cron '*/20 * * * *'
    }
    stages {
        stage('clone') {
            steps {
		git branch: 'main', url: 'https://github.com/Aakash0706/test-my-app.git'
            }
        }
        stage('Build') {
            steps {
                sh 'npm install'
                sh 'npm run build'
            }
        }
        stage('Docker Build & push') {
            steps {
                sh 'docker build -t test-my-app .'
                sh 'docker tag test-my-app jaiswalakash/test-my-app'
            }
        }
        stage('pull and run') {
            steps {
                sh 'docker pull jaiswalakash/test-my-app'
		 sh 'docker rm -f test-my-app || true'
                sh 'docker run -d -p 9091:80 jaiswalakash/test-my-app'
            }
        }
    }
}

