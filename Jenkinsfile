pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                sh 'echo building'
                // Install dependencies copy env ex to .env compile javascript assets etc.
                sh 'composer install'
                sh 'cp .env.example .env'
                sh 'php artisan key:generate'
                sh 'npm install'
               
            }
        }

        stage('Test') {
            steps {
                sh 'echo testing'
                // run the automated testing suites
                sh 'php artisan test'
            }
        }

        stage('Deploy') {
            steps {
                sh 'echo deploying'
            }
        }
    }
}