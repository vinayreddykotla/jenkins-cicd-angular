pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                sh 'ls'
                sh 'npm install'
                sh 'echo N | ng analytics off'
                sh 'ng build'
                sh 'cd dist/angular-app/browser'
                sh 'ls'
            }
        }
        stage('S3 Upload') {
            steps {
                withAWS(region: 'us-east-1', credentials: '9dc47d93-f065-48df-9d1e-562ac8922093') {
                    sh 'ls -la'
                    sh 'aws s3 cp * s3://sk-jenkins-ng/'
                }
            }
        }
    }
}
