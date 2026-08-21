stage('SonarQube Analysis') {

    agent {
        label 'sonar-agent'
    }

    options {
        skipDefaultCheckout(true)
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
            echo "SONARSCANNER"
            echo "=============================="
            which sonar-scanner
            sonar-scanner --version

            echo "=============================="
            echo "SONARQUBE STATUS"
            echo "=============================="
            curl -s http://10.100.1.6:9000/api/system/status

            echo ""
            echo "=============================="
            echo "RUNNING SONARQUBE ANALYSIS"
            echo "=============================="

            sonar-scanner \
              -Dsonar.projectKey=jenkins-ci-lab \
              -Dsonar.sources=. \
              -Dsonar.host.url=http://10.100.1.6:9000
        '''
    }
}
