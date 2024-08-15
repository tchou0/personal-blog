pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Install Tools') {
            steps {
                sh 'npm install'
            }
        }

        stage('Lint CSS') {
            steps {
                sh 'npx stylelint "**/*.css"'
            }
        }

        stage('Lint HTML') {
            steps {
                sh 'npx htmlhint "**/*.html"'
            }
        }

        stage('Deploy') {
            steps {
                // Add your deployment steps here, e.g., copying files to a server
            }
        }
    }

    post {
        always {
            archiveArtifacts artifacts: '**/*.html, **/*.css', fingerprint: true
        }
        failure {
            mail to: 'your-email@example.com',
                 subject: "Build Failed: ${currentBuild.fullDisplayName}",
                 body: "Check the Jenkins console output: ${env.BUILD_URL}"
        }
    }
}
