pipeline {
    agent any

    stages {
        stage('Build') {
            agent {
                docker {
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps {
                sh '''
                    echo "Listing files..."
                    ls -ls

                    echo "Checking npm and node versions..."
                    npm --version
                    node --version

                    echo "Installing dependencies..."
                    npm ci

                    echo "Building the project..."
                    npm run build

                    echo "Listing files after build..."
                    ls -la
                '''
            }
        }
        stage('Test') {
            agent {
                docker {
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps {
                sh '''
                    echo "Run tests..."
                    npm test
                '''
            }
        }
    }
}
