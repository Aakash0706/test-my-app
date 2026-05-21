pipeline {
    agent any
    triggers{
        cron '*/2 * * * *'
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
                sh 'docker run -d -p 8089:80 jaiswalakash/test-my-app'
            }
        }
    }
}

