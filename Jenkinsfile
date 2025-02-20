pipeline {
    agent any
    stages {
        stage('Install Dependencies') {
            steps {
                echo "Starting npm install"
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
