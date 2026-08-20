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
                echo 'Build stage running from GitHub'
            }
        }
        stage('Test') {
            steps {
                echo 'Test stage running from GitHub'
            }
        }
    }
}
