pipeline {
    agent any

    stages {
        stage('Clone') {
            steps {
                git branch: 'main', url: 'https://github.com/devika005/codedeploy-repo.git'
            }
        }

        stage('Package') {
            steps {
                sh 'zip -r app.zip .'
            }
        }

        stage('Upload to S3') {
            steps {
                sh 'aws s3 cp app.zip s3://s3bucket-devika/app.zip'
            }
        }

        stage('Deploy using CodeDeploy') {
            steps {
                sh '''
                aws deploy create-deployment \
                --application-name devika-codedeploy \
                --deployment-group-name devika-deployment-group \
                --s3-location bucket=s3bucket-devika,key=app.zip,bundleType=zip
                '''
            }
        }
    }
}
