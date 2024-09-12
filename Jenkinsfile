pipeline {
    agent any

    environment {
        NETLIFY_SITE_ID = '78edeb14-6414-4298-be7f-cbacb7fe864a'
        NETLIFY_AUTH_TOKEN = credentials('netlify-token')
    }

    stages {
        stage('Deploy!') {
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
                            # Install dependencies
                            npm install -g netlify-cli

                            # Verify the Netlify CLI version
                            netlify --version

                            # Build the project
                            npm install
                            npm run build

                            # Check deployment status
                            echo "Deploying to production, Site ID: $NETLIFY_SITE_ID"
                            netlify status

                            # Deploy to Netlify
                            netlify deploy --dir=build --prod
                            '''
                        }
                    }
                }
                // Add other parallel stages here if needed
            }
        }
    }
}
