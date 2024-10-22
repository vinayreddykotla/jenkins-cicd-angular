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
                sh 'cd dist && ls'
                sh 'cd dist/angular-tour-of-heroes/browser && ls'
            }
        }
        stage('S3 Upload') {
            steps {
                withAWS(region: 'us-east-1', credentials: '64fffe04-8914-4e4f-bc85-46252fc490c1') {
                    sh 'ls -la'
                    sh 'aws s3 cp dist/angular-tour-of-heroes/browser/. s3://angular-deploy-s3/ --recursive'
                }
            }
        }
    }
}
