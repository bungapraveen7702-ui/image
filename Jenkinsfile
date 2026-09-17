pipeline {
    agent any

    tools {
        nodejs 'node'
    }

    options {
        skipDefaultCheckout(true)
    }

    stages {

        stage('Git Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/Arun-KumarRavi/CAKE_Site.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('ESLint Analysis') {
            steps {
                sh 'npx eslint src'
            }
        }

        stage('Run Unit Tests') {
            environment {
                CI = 'true'
            }
            steps {
                sh 'npm test -- --coverage --watchAll=false'
            }
        }

        stage('Build Application') {
            environment {
                CI = 'false'
            }
            steps {
                sh 'npm run build'
            }
        }
    }
}
