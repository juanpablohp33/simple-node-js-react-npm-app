pipeline {
    agent any
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
		sh 'chmod +x ./jenkins/scripts/test.sh'
                sh './jenkins/scripts/test.sh'
            }
        }
	stage('Deliver for development') {
            when {
                branch 'development'
            }
            steps {
		sh 'chmod +x ./jenkins/scripts/deliver-for-development.sh'
                sh 'chmod +x ./jenkins/scripts/kill.sh'
		sh './jenkins/scripts/deliver-for-development.sh'
                input message: 'Finished using the web site? (Click "Proceed" to continue)'
                sh './jenkins/scripts/kill.sh'
            }
        }
	stage('Deploy for production') {
            when {
                branch 'master'
            }
            steps {
		sh 'chmod +x ./jenkins/scripts/kill.sh'
                sh 'chmod +x ./jenkins/scripts/deploy-for-production.sh'
		sh './jenkins/scripts/deploy-for-production.sh'
                input message: 'Finished using the web site? (Click "Proceed" to continue)'
                sh './jenkins/scripts/kill.sh'
            }
        }
    }
}
