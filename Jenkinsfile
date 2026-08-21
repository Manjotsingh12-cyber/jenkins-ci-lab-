stage('Check SonarScanner') {
    agent {
        label 'sonar-agent'
    }
    steps {
        sh '''
            hostname
            which sonar-scanner
            sonar-scanner --version
        '''
    }
}
