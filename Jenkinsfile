pipeline {
    agent any

    environment {
        BUILD_ENV = "production"
    }

    stages {
        stage('Checkout') {
            steps {
                retry(2) {
                    checkout scm
                }
            }
        }
        stage('Deploy') {
            when {
                environment name: 'BUILD_ENV', value: 'production'
            }
            steps {
                echo 'This only runs when BUILD_ENV is production'
            }
        }
        stage('Skip Example') {
            when {
                environment name: 'BUILD_ENV', value: 'staging'
            }
            steps {
                echo 'This only runs when BUILD_ENV is staging'
            }
        }
    }
}
