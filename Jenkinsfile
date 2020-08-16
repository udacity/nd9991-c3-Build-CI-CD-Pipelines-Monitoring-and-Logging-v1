pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                sh 'echo "Hello Mayank"'
                sh '''
                    echo "Multiline shell steps works too"
                    ls -lah
                    '''
            }
        }     
        stage('Upload to AWS') {
            steps {
                withAWS(region:'us-east-2',credentials:'aws-static') {
                    sh 'echo "Uploading content with AWS creds"'
                    s3Upload(pathStyleAccessEnabled: true, payloadSigningEnabled: true, file:'index.html', bucket:'static-mayank-jenkins-pipeline')
                }
            }
        }
        stage('Security Scan') {
            steps { 
                aquaMicroscanner imageName: 'alpine:latest', notCompleted: 'exit 1', onDisallowed: 'fail'
            }
        }    
    }
}