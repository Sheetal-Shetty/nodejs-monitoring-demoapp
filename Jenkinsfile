pipeline {
    agent any

    stages {
        stage('Install Node.js and NPM') {
            steps {
                script {
                    sh '''
                    echo "Installing Node.js and NPM..."
                    sudo apt-get update -y
                    sudo apt-get install nodejs npm -y
                    node -v
                    npm -v
                    '''
                }
            }
        }

        stage('Lint Check') {
            steps {
                script {
                    sh '''
                    echo "Running lint check..."
                    sudo make lint
                    '''
                }
            }
        }

        stage('Auto-fix Lint Issues') {
            steps {
                script {
                    sh '''
                    echo "Running lint fix..."
                    sudo make lint-fix
                    '''
                }
            }
        }

        stage('Run Tests') {
            steps {
                script {
                    sh '''
                    echo "Running tests..."
                    sudo make test
                    '''
                }
            }
        }

        stage('Generate Test Report') {
            steps {
                script {
                    sh '''
                    echo "Generating test report..."
                    sudo make test-report
                    '''
                }
            }
        }

    
        stage('Run') {
            steps {
                script {
                    sh '''
                    echo "Generating test report..."
                    sudo make run
                    '''
                }
            }
        }
    }

    post {
        success {
            echo "✅ All stages completed successfully!"
        }
        failure {
            echo "❌ Build failed. Check console output for errors."
        }
    }
}
