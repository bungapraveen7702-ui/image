pipeline{
    agent any
    stages{
        stage('checkout'){
            steps{
                checkout scm
            }
        }
        stage('Install Dependencies'){
            steps{
                sh 'npm install'
            }
        }
        stage('ESLint Analysis'){
            steps{
                sh 'npx eslint'
            }
        }
    }
}