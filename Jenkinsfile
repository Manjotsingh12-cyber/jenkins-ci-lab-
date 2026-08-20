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
        stage('Install dependencies') {
            steps {
                sh 'python3 -m venv venv'
                sh '. venv/bin/activate && pip install -r requirements.txt'
            }
        }
        stage('Unit Tests') {
            steps {
                sh '. venv/bin/activate && pytest test_app.py -v'
            }
        }
    }
}
