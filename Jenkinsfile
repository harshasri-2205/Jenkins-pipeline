pipeline {
    agent any
    tools { nodejs "node" }  // Ensure Jenkins uses the installed Node.js version
    stages {
        stage('Install Dependencies') {
            steps {
                echo "Starting npm install"
                sh 'node -v'  // Check Node.js version
                sh 'npm -v'   // Check npm version
                sh 'npm install'
            }
        }
        stage('Run Tests') {
            steps {
                echo "Running tests"
                sh 'npm test'
            }
        }
    }
}
