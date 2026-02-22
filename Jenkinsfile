pipeline {
    agent any
 
    environment {
        // Prendi l'App ID da AppScan on Cloud → Applications
        APPSCAN_APP_ID = '2dd05bbd-6429-4d47-9228-af780c48bc7e'
        APPSCAN_CREDENTIALS = 'appscan-cloud-credentials'
    }
 
    stages {
 
        stage('Checkout') {
            steps {
                checkout scm
                echo '✅ Codice scaricato da GitHub'
            }
        }
 
        stage('AppScan SAST') {
            steps {
                echo '🔍 Avvio scansione SAST con AppScan on Cloud...'
                appscan(
                    application: "${APPSCAN_APP_ID}",
                    credentials: "${APPSCAN_CREDENTIALS}",
                    scanner: static_analyzer(
                        target: '.',
                        hasOptions: false
                    ),                                  
                    name: "SAST-${env.BUILD_NUMBER}",
                    wait: true,
                    failBuildNonCompliance: true,
                    failBuild: false
                )
            }
