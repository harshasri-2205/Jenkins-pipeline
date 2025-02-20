pipeline {
    agent any
    tools { nodejs "node" }  // Ensure Jenkins uses the installed Node.js version
    environment {
        imageName = "harsha2001/react-app"
        registryCredentials = credentials('harsha2001')
        dockerImage = ""
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
                echo "Building image"
               dockerImage = docker.build imageName
            }
        }
        stage('Deploy Image') {
            steps {
                echo "Deploying image"
                docker.withRegistry('https://registry.hub.docker.com', 'dockerhub-cred') {
                    dockerImage.push(${env.BUILD_NUMBER})
                }
            }
        }
    }
}
