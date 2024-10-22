pipeline {
    agent any

    environment {
        NODEJS_VERSION = 'node14'  // Node.js version to be used
    }

    stages {

        stage('Install Node.js and Angular CLI') {
            steps {
                script {
                    def nodejs = tool name: "${NODEJS_VERSION}", type: 'NodeJSInstallation'
                    env.PATH = "${nodejs}/bin:${env.PATH}"
                }
                // Verify Node.js and npm are available
                sh 'node -v'
                sh 'npm -v'
                
                // Install Angular CLI globally if not installed
                sh 'npm install -g @angular/cli'
            }
        }

        stage('Build Angular App') {
            steps {
                // Ensure the app's directory has necessary files
                sh 'ls'
                
                // Install project dependencies
                sh 'npm install'

                // Disable Angular CLI analytics
                sh 'echo N | ng analytics off'

                // Build the Angular app in production mode
                sh 'ng build --prod'

                // Check the distribution folder for the build output
                sh 'ls dist'
                sh 'cd dist/angular-tour-of-heroes/browser && ls'
            }
        }

        stage('S3 Upload') {
            steps {
                withAWS(region: 'us-east-1', credentials: '592b34f4-4d36-4cea-9638-83b9a06d9b3d') {
                    // Ensure the build files are ready
                    sh 'ls -la'

                    // Upload the built Angular app to the S3 bucket
                    sh 'aws s3 cp dist/angular-tour-of-heroes/browser/. s3://angular-deploy-s3/ --recursive'
                }
            }
        }
    }

    post {
        success {
            echo 'Build and deployment succeeded!'
        }
        failure {
            echo 'Build or deployment failed.'
        }
    }
}
