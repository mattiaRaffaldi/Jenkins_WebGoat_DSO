pipeline {
    agent any

    environment {
        APPSCAN_APP_ID = '2dd05bbd-6429-4d47-9228-af780c48bc7e'
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/mattiaRaffaldi/Jenkins_WebGoat_DSO.git'
            }
        }

        stage('SAST - Static Analysis') {
            steps {
                appscan application: "${APPSCAN_APP_ID}",
                    credentials: 'appscan',
                    name: "SAST-${env.BUILD_NUMBER}",
                    scanner: static_analyzer(
                        hasOptions: true,
                        scanSpeed: 'fast',
                        target: 'src'
                    ),
                    type: 'Static Analyzer'
            }
        }

        stage('SCA - Software Composition Analysis') {
            steps {
                appscan application: "${APPSCAN_APP_ID}",
                    credentials: 'appscan',
                    name: "SCA-${env.BUILD_NUMBER}",
                    scanner: software_composition_analyzer(
                        target: '.'
                    ),
                    type: 'Software Composition Analysis'
            }
        }
    }

    post {
        success {
            echo 'Scansioni di sicurezza completate!'
        }
        failure {
            echo 'Build fallita — controlla i risultati delle scansioni'
        }
    }
}
