pipeline {
    agent any

    stages {
        parallel {
            stage('Build') {
                agent {
                    docker {
                        image 'node:18-alpine'
                    }
                }
                steps {
                    sh '''
                        ls -la
                        node --version
                        npm --version
                        npm ci 
                        npm run build
                        ls -la
                    '''
                }
            }

            stage('E2E') {
                agent {
                    docker {
                        image 'mcr.microsoft.com/playwright:v1.47.0-noble'
                    }
                }
                steps {
                    sh '''
                        npm install -g serve
                        serve -s build &
                        sleep 10
                        npx playwright test
                    '''
                }
            }
        }
    }
}
