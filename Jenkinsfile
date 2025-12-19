pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                git 'https://github.com/TON_USERNAME/mini-jenkins-web.git'
            }
        }

        stage('Build') {
            steps {
                echo 'Building static website...'
            }
        }

        stage('Test') {
            steps {
                echo 'Testing if index.html exists'
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
                echo 'Deploying website'
                bat '''
                if not exist deployed_site mkdir deployed_site
                copy index.html deployed_site\\
                '''
            }
        }
    }

    post {
        success {
            echo 'CI/CD pipeline completed successfully ✅'
        }
        failure {
            echo 'CI/CD pipeline failed ❌'
        }
    }
}
