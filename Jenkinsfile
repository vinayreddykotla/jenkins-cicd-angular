pipeline {
    agent any 
    environment {
        AWS_ACCESS_KEY_ID = 'AKIA4MTWMFZO445OUGFE'
        AWS_SECRET_ACCESS_KEY = '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'
        S3_BUCKET = 'angular-deploy-s3'
    }
    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/vinayreddykotla/jenkins-cicd-angular.git'
            }
        }
        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }
        stage('Build') {
            steps {
                sh 'ng build --prod'
            }
        }
        stage('Deploy to S3') {
            steps {
                script {
                    sh 'aws s3 sync ./dist/ s3://angular-deploy-s3/ --delete'
                }
            }
        }
    }
}
