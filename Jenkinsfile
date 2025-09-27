pipeline {
    agent {
        docker { image 'node:20' }
    }
    options {
        skipDefaultCheckout() // Prevent Jenkins auto checkout
    }
    stages {
        stage('Checkout') {
            steps {
                // Clone repo manually
                checkout([$class: 'GitSCM',
                    branches: [[name: '*/main']],
                    userRemoteConfigs: [[
                        url: 'https://github.com/9999-san/8.2CDevSecOps.git'
                    ]]
                ])
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
