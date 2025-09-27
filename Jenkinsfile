pipeline {
    agent {
        docker { image 'node:20' }
    }
    options {
        skipDefaultCheckout() // Avoid Jenkins trying an automatic checkout
    }
    stages {
        stage('Checkout') {
            steps {
                // Explicit clone, ensures .git exists
                sh 'git clone -b main https://github.com/9999-san/8.2CDevSecOps.git repo'
                dir('repo') {
                    sh 'git status' // Confirm repo exists
                }
            }
        }
        stage('Install Dependencies') {
            steps {
                dir('repo') {
                    sh 'npm install'
                }
            }
        }
        stage('Run Tests') {
            steps {
                dir('repo') {
                    sh 'npm test || true'
                }
            }
        }
        stage('Generate Coverage Report') {
            steps {
                dir('repo') {
                    sh 'npm run coverage || true'
                }
            }
        }
        stage('NPM Audit (Security Scan)') {
            steps {
                dir('repo') {
                    sh 'npm audit || true'
                }
            }
        }
    }
}
