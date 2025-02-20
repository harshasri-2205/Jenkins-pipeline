pipeline {
    agent any
    tools { nodejs "node" }  // Ensure Jenkins uses the installed Node.js version
    environment {
        imageName = "harsha2001/react-app"
        registryCredentials = 'dockerhub-cred'  // Use correct credentials ID
    }

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
        stage('Build Image') {
            steps {
                script {
                    echo "Building Docker image"
                    dockerImage = docker.build("${imageName}:${env.BUILD_NUMBER}")
                }
            }
        }
        stage('Deploy Image') {
            steps {
                script {
                    echo "Deploying image"
                    docker.withRegistry('https://registry.hub.docker.com', registryCredentials) {
                        dockerImage.push("${env.BUILD_NUMBER}")
                        dockerImage.push("latest")  // Push as latest for easier deployment
                    }
                }
            }
        }
    }
}
