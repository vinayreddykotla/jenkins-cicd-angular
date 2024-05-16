pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                sh 'ls'
                sh 'npm install'
                sh 'echo N | ng analytics off'
                sh 'ng build'
                sh 'ls'
                sh 'cd dist'
                sh 'ls'
                sh 'cd dist/angular-app/browser'
                sh 'ls'
            }
        }
        stage('S3 Upload') {
            steps {
                withAWS(region: 'us-east-1', credentials: '887a4efb-0f53-4929-8ac6-f425dae11daa') {
                    sh 'ls -la'
                    sh 'aws s3 cp * s3://sk-jenkins-ng/'
                }
            }
        }
    }
}
