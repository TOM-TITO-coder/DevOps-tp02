pipeline {
    agent any

    environment {
        // Telegram configuration
        TOKEN = credentials('6649100675:AAHb--EZYBCeWdw4m6uUXlI5TqWYUCNEAuY')
        CHAT_ID = credentials('987537983')
    }
    
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
        success {
            script {
                bat "curl -X POST -H \"Content-Type: application/json\" -d \"{\\\"chat_id\\\":${CHAT_ID}, \\\"text\\\": \\\"Pipeline succeeded!\\\", \\\"disable_notification\\\": false}\" https://api.telegram.org/bot${TOKEN}/sendMessage"
            }
        }
        failure {
            script {
                bat "curl -X POST -H \"Content-Type: application/json\" -d \"{\\\"chat_id\\\":${CHAT_ID}, \\\"text\\\": \\\"Pipeline failed!\\\", \\\"disable_notification\\\": false}\" https://api.telegram.org/bot${TOKEN}/sendMessage"
            }
        }
    }
    
}
