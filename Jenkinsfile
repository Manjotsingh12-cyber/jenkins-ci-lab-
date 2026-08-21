pipeline {
    agent any

    stages {

        stage('Check SonarScanner') {
            agent {
                label 'sonar-agent'
            }

            steps {
                sh '''
                    echo "=== Hostname ==="
                    hostname

                    echo "=== SonarScanner Location ==="
                    which sonar-scanner

                    echo "=== SonarScanner Version ==="
                    sonar-scanner --version

                    echo "=== SonarQube Connectivity ==="
                    curl -s http://10.100.1.6:9000/api/system/status
                '''
            }
        }

    }
}
