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
        stage('Show Environment') {
            steps {
                sh 'echo "App name is: $APP_NAME"'
                sh 'echo "Build env is: $BUILD_ENV"'
                sh 'echo "Jenkins build number is: $BUILD_NUMBER"'
            }
        }
    }
}
