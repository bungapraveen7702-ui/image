pipeline {
    agent any

    tools {
        nodejs 'node'
    }

    stages {
        stage('Git Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/Arun-KumarRavi/CAKE_Site.git'
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

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('SonarQube-Server') {
                    sh '''
                        npx sonarqube-scanner \
                          -Dsonar.projectKey=SP-Cakes-Site \
                          -Dsonar.projectName="SP Cakes & Delight" \
                          -Dsonar.sources=src \
                          -Dsonar.tests=src \
                          -Dsonar.test.inclusions="**/*.test.js" \
                          -Dsonar.exclusions="**/*.test.js,**/node_modules/**" \
                          -Dsonar.javascript.lcov.reportPaths=coverage/lcov.info
                    '''
                }
            }
        }

        stage('SonarQube Quality Gate') {
            steps {
                timeout(time: 5, unit: 'MINUTES') {
                    waitForQualityGate abortPipeline: true
                }
            }
        }

        stage('Trivy FileSystem Scan') {
            steps {
                sh '''
                    trivy fs \
                      --scanners vuln,secret,misconfig \
                      --severity HIGH,CRITICAL \
                      --exit-code 0 \
                      --format table \
                      .
                '''
            }
        }

        stage('Build Application') {
            environment {
                // Setting CI=false prevents Create React App from failing builds on non-fatal warnings
                CI = 'false'
            }
            steps {
                sh 'npm run build'
            }
        }
    }
}
