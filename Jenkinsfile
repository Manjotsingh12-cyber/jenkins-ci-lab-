pipeline {
    agent any

    options {
        skipDefaultCheckout(true)
    }

    stages {

        stage('Checkout') {
            steps {
                checkout scm

                stash name: 'source-code',
                      includes: '**/*',
                      useDefaultExcludes: false
            }
        }

        stage('Check SonarScanner') {
            agent {
                label 'sonar-agent'
            }

            steps {
                deleteDir()

                unstash 'source-code'

                sh '''
                    echo "=============================="
                    echo "HOSTNAME"
                    echo "=============================="
                    hostname

                    echo "=============================="
                    echo "SONARSCANNER LOCATION"
                    echo "=============================="
                    which sonar-scanner

                    echo "=============================="
                    echo "SONARSCANNER VERSION"
                    echo "=============================="
                    sonar-scanner --version

                    echo "=============================="
                    echo "SONARQUBE CONNECTION"
                    echo "=============================="
                    curl -s http://10.100.1.6:9000/api/system/status
                '''
            }
        }
    }
}
