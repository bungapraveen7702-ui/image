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
                sh 'npm eslint src'
            }
        }

        stage('Run Unit Tests') {
            steps {
                sh 'npm test'
            }
        }
    }
}
