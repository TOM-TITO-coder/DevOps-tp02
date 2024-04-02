pipeline {
    agent any
    
    stages {
        stage('Install Dependencies') {
            steps {
                sh 'composer install'
                sh 'php artisan key:generate'
                sh 'npm install'
            }
        }
        stage('Build') {
            steps {
                sh 'npm '
            }
        }
        
    }
    post {
        failure {
            telegramSend(
                message: "Pipeline Failed: ${currentBuild.fullDisplayName}. Please check the Jenkins console output for more details.",
                chatId: "987537983"
            )
        }
    }
    
}
