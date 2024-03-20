pipeline {
    agent any
    stages {
        stage('Grype scan') {
            steps {
                grypeScan scanDest: 'dir:.', repName: 'myScanResult.txt', autoInstall:true
            }
        }
    }
    post {
        always {
            // Publish HTML report
            publishHTML([
                allowMissing: false,
                alwaysLinkToLastBuild: true,
                keepAll: true,
                reportDir: '.',
                reportFiles: 'myScanResult.txt',
                reportName: 'Grype Scan Report'
            ])
        }
    }
}
