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
        stage('End stage'){
            steps{
                
            }
        }
    }
    
}
