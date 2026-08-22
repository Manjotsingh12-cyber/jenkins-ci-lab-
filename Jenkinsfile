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

        stage('Secret Scan') {
            steps {
                sh 'gitleaks git -v --exit-code 1'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'python3 -m venv venv'
                sh '. venv/bin/activate && pip install -r requirements.txt'
            }
        }

        stage('Lint') {
            steps {
                sh '. venv/bin/activate && flake8 app.py test_app.py --max-line-length=100'
            }
        }

        stage('Unit Tests') {
            steps {
                sh '. venv/bin/activate && pytest test_app.py -v'
            }
        }

        stage('Docker Build') {
            steps {
                sh 'docker build -t jenkins-ci-lab:$BUILD_NUMBER .'
            }
        }

        stage('Verify Image') {
            steps {
                sh 'docker images | grep jenkins-ci-lab'
            }
        }

        stage('Trivy Scan') {
            steps {
                sh 'trivy image --exit-code 0 --severity HIGH,CRITICAL jenkins-ci-lab:$BUILD_NUMBER'
            }
        }

        stage('Push to ECR') {
            steps {
                sh '''
                    aws ecr get-login-password --region ap-south-1 | docker login --username AWS --password-stdin 991362938746.dkr.ecr.ap-south-1.amazonaws.com
                    docker tag jenkins-ci-lab:$BUILD_NUMBER 991362938746.dkr.ecr.ap-south-1.amazonaws.com/jenkins-ci-lab:$BUILD_NUMBER
                    docker push 991362938746.dkr.ecr.ap-south-1.amazonaws.com/jenkins-ci-lab:$BUILD_NUMBER
                '''
            }
        }
    }
}
