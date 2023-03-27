pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                sh 'composer install'
                sh 'npm install'
                sh 'npm run build'
                // and other necessary commands to compile your assets
            }
        }
        stage('Test') {
            steps {
                sh 'php artisan test'
            }
        }
        
        stage('Deploy to staging') {
            steps {
                sh 'ssh deploy@192.168.2.40 -o StrictHostKeyChecking=no "bash /var/www/larademo/scripts/deploy.sh" '
            }
        }

        stage('Deploy to production') {
            steps {
                sh 'ssh dare@165.22.235.232 -o StrictHostKeyChecking=no "bash /var/www/larademo/scripts/deploy.sh" '
            }
        }
    }

    // apply to the whole pipeline

    post {
     // send email notification the specicied addresses if the build fails
        failure {  
             mail bcc: '', body: "<b>Failed Jenkins Build</b><br>Project: ${env.JOB_NAME} \
             <br>Build Number: ${env.BUILD_NUMBER} <br> URL of the build: ${env.BUILD_URL}", cc: '', \
             charset: 'UTF-8', from: 'jenkins@jenkins.test', mimeType: 'text/html', replyTo: 'put@youremail.com', \
             subject: "ERROR CI: Project name -> ${env.JOB_NAME}", \
             to: "failure@jenkinsbuild.com";  \
         }
    }

}