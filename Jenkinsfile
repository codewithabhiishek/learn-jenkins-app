pipeline {
    agent any

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
                            '''
                        }
                    }
                }
                // Add other parallel stages here if needed
            }
        }
    }
}
