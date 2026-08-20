pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                retry(3) {
                    checkout scm
                }
            }
        }
        stage('Hello') {
            steps {
                echo 'Pipeline is working'
            }
        }
    }
}
