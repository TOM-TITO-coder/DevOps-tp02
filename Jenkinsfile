pipeline {
    agent any

    environment {
        // Define environment variables
        TOKEN = credentials('6649100675:AAHb--EZYBCeWdw4m6uUXlI5TqWYUCNEAuY')
        CHAT_ID = credentials('987537983')

        CURRENT_BUILD_NUMBER = "${currentBuild.number}"
        GIT_MESSAGE = sh(returnStdout: true, script: "git log -n 1 --format=%s ${GIT_COMMIT}").trim()
        GIT_AUTHOR = sh(returnStdout: true, script: "git log -n 1 --format=%ae ${GIT_COMMIT}").trim()
        GIT_COMMIT_SHORT = sh(returnStdout: true, script: "git rev-parse --short ${GIT_COMMIT}").trim()
        GIT_INFO = "Branch(Version): ${GIT_BRANCH}\nLast Message: ${GIT_MESSAGE}\nAuthor: ${GIT_AUTHOR}\nCommit: ${GIT_COMMIT_SHORT}"
        TEXT_BREAK = "--------------------------------------------------------------"
        TEXT_PRE_BUILD = "${TEXT_BREAK}\n${GIT_INFO}\n${JOB_NAME} is Building"
        TEXT_SUCCESS_BUILD = "${JOB_NAME} is Success"
        TEXT_FAILURE_BUILD = "${JOB_NAME} is Failure"
    }

    stages {
        stage('Install Dependencies') {
            steps {
                {
                    // Enclose shell commands inside a node block
                    sh 'composer install'
                    sh 'php artisan key:generate'
                    sh 'npm install'
                }
            }
        }
        stage('Build') {
            steps {
                {
                    sh 'npm run'
                }
            }
        }
    }

    post {
        success {
            script {
                // Enclose curl command inside a node block
                sh "curl -X POST -H 'Content-Type: application/json' -d '{\"chat_id\": \"${CHAT_ID}\", \"text\": \"${TEXT_SUCCESS_BUILD}\", \"disable_notification\": false}' https://api.telegram.org/bot${TOKEN}/sendMessage"
            }
        }
        failure {
            script {
                // Enclose curl command inside a node block
                sh "curl -X POST -H 'Content-Type: application/json' -d '{\"chat_id\": \"${CHAT_ID}\", \"text\": \"${TEXT_FAILURE_BUILD}\", \"disable_notification\": false}' https://api.telegram.org/bot${TOKEN}/sendMessage"
            }
        }
    }
}
