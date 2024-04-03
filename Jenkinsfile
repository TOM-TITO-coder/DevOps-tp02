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
        // Define environment variables
        def TOKEN = credentials('6649100675:AAHb--EZYBCeWdw4m6uUXlI5TqWYUCNEAuY')
        def CHAT_ID = credentials('987537983')
        def TEXT_SUCCESS_BUILD = "${JOB_NAME} is Success"

        // Send success message
        sh "curl -X POST -H 'Content-Type: application/json' -d '{\"chat_id\": \"${CHAT_ID}\", \"text\": \"${TEXT_SUCCESS_BUILD}\", \"disable_notification\": false}' https://api.telegram.org/bot${TOKEN}/sendMessage"
      }
    }
    failure {
      script {
        // Define environment variables
        def TOKEN = credentials('6649100675:AAHb--EZYBCeWdw4m6uUXlI5TqWYUCNEAuY')
        def CHAT_ID = credentials('987537983')
        def TEXT_FAILURE_BUILD = "${JOB_NAME} is Failure"

        // Send failure message
        sh "curl -X POST -H 'Content-Type: application/json' -d '{\"chat_id\": \"${CHAT_ID}\", \"text\": \"${TEXT_FAILURE_BUILD}\", \"disable_notification\": false}' https://api.telegram.org/bot${TOKEN}/sendMessage"
      }
    }
  }
}
