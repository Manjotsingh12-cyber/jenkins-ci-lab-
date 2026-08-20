pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Build stage running from GitHub'
            }
        }
        stage('Test') {
            steps {
                echo 'Test stage running from GitHub'
            }
        }
        stage('Verify Checkout Works') {
            steps {
                sh 'git log -1 --oneline'
                sh 'ls -la'
                sh 'echo "Timing test run"'
            }
        }
    }
}
