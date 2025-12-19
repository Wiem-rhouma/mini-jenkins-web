pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git(
                    url: 'https://github.com/Wiem-rhouma/mini-jenkins-web.git',
                    credentialsId: 'github-token',
                    branch: 'main'
                )
            }
        }

        stage('Build') {
            steps { echo 'Building static website...' }
        }

        stage('Test') {
            steps {
                bat '''
                if exist index.html (
                    echo index.html exists
                ) else (
                    echo index.html missing
                    exit /b 1
                )
                '''
            }
        }

        stage('Deploy') {
            steps {
                bat '''
                if not exist deployed_site mkdir deployed_site
                copy index.html deployed_site\\
                '''
            }
        }
    }

    post {
        success { echo 'CI/CD pipeline completed successfully ✅' }
        failure { echo 'CI/CD pipeline failed ❌' }
    }
}
