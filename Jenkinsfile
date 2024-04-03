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
      script{
        sh "curl --location --request POST 'https://api.telegram.org/bot6649100675:AAHb--EZYBCeWdw4m6uUXlI5TqWYUCNEAuY/sendMessage' --form text='${TEXT_SUCCESS_BUILD}' --form chat_id='987537983'"
      }
    }
    failure {
      script{
        sh "curl --location --request POST 'https://api.telegram.org/bot6649100675:AAHb--EZYBCeWdw4m6uUXlI5TqWYUCNEAuY/sendMessage' --form text='${TEXT_FAILURE_BUILD}' --form chat_id='987537983'"
      }
    }
  }
}
