pipeline {
    agent any
    tools {nodejs "nodejs22"}
    environment {
        CI = 'true'
    }
    stages {
        stage('Build') {
            steps {
                sh 'npm install'
            }
        }
        stage('Test') {
            steps {
                sh './jenkins/scripts/test.sh'
            }
        }
        stage('Deliver to Development') {
            when {
                branch 'development'
            }
            steps {
                sh './jenkins/scripts/deliver-for-development'
                input message: 'Finsihed using website, (Click "Proceed" to continue)'
                sh '/.jenkins/scripts/kill.sh'
            }
        }
        stage('Deploy to production') {
            when {
                branch 'production'
            }
            steps {
                sh './jenkins/scripts/deploy-for-production'
                input message: 'Finsihed using website, (Click "Proceed" to continue)'
                sh './jenkins/scripts/kill.sh'
            }
        }
    }
}
