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
        
        stage('Deploy') {
            steps {
                sh 'ssh deploy@192.168.2.40 -o StrictHostKeyChecking=no "bash /var/www/larademo/scripts/deploy.sh" '
            }
        }
    }
}