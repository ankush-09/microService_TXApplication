pipeline {
    agent any
    stages {
        stage('Grype scan') {
            steps {
                grypeScan scanDest: 'dir:.', repName: 'myScanResult.txt', autoInstall:true
            }
        }
        stage('Publish Report') {
            steps {
                // Archive the Grype scan report as an artifact
                archiveArtifacts artifacts: 'myScanResult.txt', onlyIfSuccessful: true
            }
        }
    }
    post {
        always {
            // Record issues and aggregate results
            recordIssues(
                tools: [grype()],
                aggregatingResults: true
            )
        }
    }
}
