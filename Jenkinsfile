pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                retry(2) {
                    checkout scm
                }
            }
        }
        stage('Build') {
            steps {
                echo 'Build stage running from GitHub - webhook test'
            }
        }
        stage('Test') {
            steps {
                echo 'Test stage running from GitHub'
            }
        }
        stage('Confirm Webhook Trigger') {
            steps {
                sh 'echo "This build should have started automatically, not manually"'
                sh 'date'
            }
        }
    }
}
