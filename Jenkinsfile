pipeline {
    agent any
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
                appscan application: '2dd05bbd-6429-4d47-9228-af780c48bc7e',
                         credentials: 'appscan',
                         name: "SAST-${env.BUILD_NUMBER}",
                         scanner: static_analyzer(hasOptions: true, scanSpeed: 'fast', target: '.'),
                         type: 'Static Analyzer'
            }
        }
    }
    post {
        success {
            echo '✅ Security Gate SUPERATO'
        }
        failure {
            echo '❌ BUILD FALLITO — Vulnerabilità critiche rilevate!'
        }
    }
}