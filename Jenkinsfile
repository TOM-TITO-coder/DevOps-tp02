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
        sh 'npm run build'
      }
    }
  }

  post {
    success {
      script {
        sh 'curl -X POST -H "Content-Type: application/json" -d "{\"chat_id\": \"987537983\", \"text\": \"Pipeline succeeded!\", \"disable_notification\": false}" https://api.telegram.org/bot6649100675:AAHb--EZYBCeWdw4m6uUXlI5TqWYUCNEAuY/sendMessage'
      }
    }
    failure {
      script {
        sh 'curl -X POST -H "Content-Type: application/json" -d "{\"chat_id\": \"987537983\", \"text\": \"Pipeline failed!\", \"disable_notification\": false}" https://api.telegram.org/bot6649100675:AAHb--EZYBCeWdw4m6uUXlI5TqWYUCNEAuY/sendMessage'
      }
    }
  }
}
