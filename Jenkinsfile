pipeline {

    agent none

    stages {

        stage('Checkout') {
            agent { label 'built-in' }

            steps {
                checkout scm

                stash name: 'source-code', includes: '**/*', useDefaultExcludes: false
            }
        }

        stage('Check SonarScanner') {
            agent { label 'sonar-agent' }

            steps {
                deleteDir()

                unstash 'source-code'

                sh '''
                    echo "=============================="
                    echo "HOSTNAME"
                    echo "=============================="
                    hostname

                    echo "=============================="
                    echo "SONARSCANNER"
                    echo "=============================="
                    which sonar-scanner
                    sonar-scanner --version

                    echo "=============================="
                    echo "SONARQUBE CONNECTION"
                    echo "=============================="
                    curl --fail --max-time 10 \
                        http://10.100.1.6:9000/api/system/status
                '''
            }
        }

        stage('Python Tests') {
            agent { label 'sonar-agent' }

            steps {
                sh '''
                    echo "=============================="
                    echo "PYTHON TESTS"
                    echo "=============================="

                    python3 --version

                    python3 -m venv venv

                    ./venv/bin/pip install --upgrade pip
                    ./venv/bin/pip install pytest flask

                    ./venv/bin/pytest -v
                '''
            }
        }

        stage('SonarQube Analysis') {
            agent { label 'sonar-agent' }

            steps {
                sh '''
                    echo "=============================="
                    echo "SONARQUBE ANALYSIS"
                    echo "=============================="

                    sonar-scanner \
                      -Dsonar.projectKey=jenkins-ci-lab \
                      -Dsonar.projectName=jenkins-ci-lab \
                      -Dsonar.sources=. \
                      -Dsonar.host.url=http://10.100.1.6:9000
                '''
            }
        }

        stage('Docker Build') {
            agent { label 'sonar-agent' }

            steps {
                sh '''
                    echo "=============================="
                    echo "DOCKER BUILD"
                    echo "=============================="

                    docker build -t jenkins-ci-lab:latest .
                '''
            }
        }

        stage('Verify Image') {
            agent { label 'sonar-agent' }

            steps {
                sh '''
                    echo "=============================="
                    echo "DOCKER IMAGE"
                    echo "=============================="

                    docker images jenkins-ci-lab

                    docker inspect jenkins-ci-lab:latest > /dev/null

                    echo "Docker image verified successfully."
                '''
            }
        }

        stage('Trivy Scan') {
            agent { label 'sonar-agent' }

            steps {
                sh '''
                    echo "=============================="
                    echo "TRIVY SECURITY SCAN"
                    echo "=============================="

                    trivy image \
                      --severity HIGH,CRITICAL \
                      --exit-code 1 \
                      jenkins-ci-lab:latest
                '''
            }
        }

        stage('Push to ECR') {
            agent { label 'sonar-agent' }

            steps {
                echo 'ECR push will be configured after the security pipeline is working.'
            }
        }
    }

    post {
        success {
            echo '================================'
            echo 'PIPELINE SUCCESS'
            echo '================================'
        }

        failure {
            echo '================================'
            echo 'PIPELINE FAILED'
            echo '================================'
        }
    }
}
