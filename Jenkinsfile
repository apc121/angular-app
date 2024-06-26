pipeline {
    agent any
    environment {
        AWS_ACCESS_KEY_ID = credentials('your-aws-access-key-id')
        AWS_SECRET_ACCESS_KEY = credentials('aws-secret-access-key')
    }
   
    stages {
        stage('Build') {
            steps {
                sh 'npm install'
                sh 'npm run build'
            }
        }

        stage('Deploy to S3') {
            steps {
                withCredentials([
                    string(credentialsId: 'your-aws-access-key-id', variable: 'AWS_ACCESS_KEY_ID'),
                    string(credentialsId: 'aws-secret-access-key', variable: 'AWS_SECRET_ACCESS_KEY')
                ]) {
                    // Use the 'aws s3 cp' command to upload the files
                    sh '''
                    aws s3 cp dist/ s3://mybucket-12121/ --recursive
                    '''
                }
            }
        }
    }

    post {
        success {
            echo 'Deployment to S3 successful!'
        }
        failure {
            echo 'Deployment to S3 failed'
        }
    }
}
