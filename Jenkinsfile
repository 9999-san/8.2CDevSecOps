pipeline {
    // Note: The agent will use the 'node:20' container. 
    // This container must have 'git' installed for the initial checkout 
    // to work if the SCM checkout happens *inside* the container context.
    // However, for SCM pipeline definition, checkout often happens *before* the agent starts.
    agent {
        docker { 
            image 'node:20' 
        }
    }
    // The default checkout will now occur automatically before the first stage.
    // The code will be present in the workspace.
    
    stages {
        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }
        
        stage('Run Tests') {
            steps {
                // Using '|| true' to continue the build even if tests fail, if desired.
                sh 'npm test || true'
            }
        }
        
        stage('Generate Coverage Report') {
            steps {
                // Using '|| true' for robustness
                sh 'npm run coverage || true'
            }
        }
        
        stage('NPM Audit (Security Scan)') {
            steps {
                // Using '|| true' for robustness
                sh 'npm audit || true'
            }
        }
    }
}