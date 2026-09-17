pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('ESLint Analysis') {
            steps {
                sh 'npx eslint .'
            }
        }

        stage('Check Project Structure') {
            steps {
                sh 'pwd'
                sh 'ls -la'
                sh 'find . -maxdepth 2 -type d'
            }
        }

        stage('Run Unit Tests') {
            steps {
                sh 'npm test'
            }
        }
    }
}