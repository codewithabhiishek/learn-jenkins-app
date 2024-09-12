pipeline {
    agent any

    environment {
        NETLIFY_SITE_ID = '78edeb14-6414-4298-be7f-cbacb7fe864a'
        NETLIFY_AUTH_TOKEN = credentials('netlify-token')
    }

    stages {
        stage('Deploy') {
            parallel {
                stage('Build') {
                    agent {
                        docker {
                            image 'node:18-alpine'
                            reuseNode true
                        }
                    }
                    steps {
                        script {
                            sh '''
                            npm install -g netlify-cli
                            netlify --version
                            echo "Deploying to production, Site ID: $NETLIFY_SITE_ID"
                            netlify status
                            '''
                        }
                    }
                }
                // Add other parallel stages here if needed
            }
        }
    }
}
