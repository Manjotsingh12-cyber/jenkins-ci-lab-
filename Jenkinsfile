pipeline {
    agent any

    environment {
        APP_NAME = "jenkins-ci-lab"
        BUILD_ENV = "staging"
    }

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
                echo 'Build stage running'
            }
        }
        stage('Deploy to Production') {
            when {
                environment name: 'BUILD_ENV', value: 'production'
            }
            steps {
                echo 'Deploying to production!'
            }
        }
    }
}
