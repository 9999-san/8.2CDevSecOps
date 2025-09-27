pipeline {
    agent {
        docker { image 'node:20' } // use an official Node.js image
    }
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/9999-san/8.2CDevSecOps'
            }
        }
        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }
        stage('Run Tests') {
            steps {
                sh 'npm test || true'
            }
        }
        stage('Generate Coverage Report') {
            steps {
                sh 'npm run coverage || true'
            }
        }
        stage('NPM Audit (Security Scan)') {
            steps {
                sh 'npm audit || true'
            }
        }
    }
}
