pipeline {
    agent any
    stages {
        stage('Git checkout') {
            steps {
                checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/ankush-09/microService_TXApplication.git']])
            }
        }
        stage('Grype scan') {
            steps {
                echo ${WORKSPACE}
            }
        }
        stage('Grype scan') {
            steps {
                grypeScan scanDest: 'dir:${WORKSPACE}', repName: 'myScanResult.txt', autoInstall:true
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
