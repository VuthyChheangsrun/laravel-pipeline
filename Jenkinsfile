pipeline {
    agent any // windows agent, Jenkins-Laravel (other machine)
    
    stages {
        stage('Fetch from GitHub') { // build steps
            steps {
                echo 'Fetching from GitHub'
                gits branch: 'main', url:'https://github.com/VuthyChheangsrun/laravel-pipeline.git'
            }
        }
        stage('Build using Tools') {
            steps {
                echo 'Compiling code...'
                sh 'cp .env.example .env'
                sh 'composer install && php artisan key:generate && npm install && npm run build'
            }
        }
        stage('Test the app') {
            steps {
                echo 'Testing unit tests...'
                echo 'Testing features...'
                sh 'php artisan test'
            }
        }
    }
    post {
        success {
            echo 'Run was Successful'  
        }
        failure {
            // emailext body: "${cat env.BUILD_URL}",
            // recipientProviders: [[$class: 'DevelopersRecipientProvider'],
            // [$class: 'RequesterRecipientProvider']],
            // from: 'address not configured yet  <nobody@nowhere>',
            // mimeType: 'text/plain',
            // replyTo: 'jenkins@gmail.com',
            // subject: "Build fail in jenkins: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
            // to: "mailtrap@gmail.com";


            mail bcc: '',
            body: "See <${env.BUILD_URL}display/redirect>\n\nChanges:\n\n\n------------------------------------------\n ${env.BUILD_URL}",
            cc: '',
            charset: 'UTF-8',
            from: 'address not configured yet  <nobody@nowhere>',
            mimeType: 'text/plain',
            replyTo: 'jenkins@gmail.com',
            subject: "Build fail in jenkins: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
            to: "mailtrap@gmail.com";  
        }
    }  
}