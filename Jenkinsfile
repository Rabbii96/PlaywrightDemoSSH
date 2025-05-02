pipeline {
    agent any

    stages {
        stage('Checkout Code') {
            steps {
                checkout scm
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm ci'
                sh 'npx playwright install'
            }
        }

        stage('Run Playwright Tests') {
            steps {
                sh 'npx playwright test --project=chromium'
            }
        }
    }

    post {
        always {
            archiveArtifacts artifacts: 'test-results/**/*.xml', allowEmptyArchive: true
            junit 'test-results/**/*.xml'
        }
        failure {
            echo '❌ Test failed!'
        }
        success {
            echo '✅ Tests passed!'
        }
    }
}
