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
        stage('Confirm Checkout') {
            steps {
                sh 'echo "Checkout succeeded"'
                sh 'git log -1 --oneline'
                sh 'ls -la'
            }
        }
    }
}
