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
                sh 'npx eslint'
            }
        }
        stage('Tests'){
            steps{
                sh 'npm test'
            }
        }
    }
}