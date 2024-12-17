pipeline {
    agent any

    stages {
        stage('Build') {
            agent {
                docker {
                    image 'node:19-alpine'
                    reuseNode true
                }
            }

            steps {
                sh '''
                    echo 'Begin build steps'
                    ls -la
                    node --version  
                    npm ci
                    npm run build
                    ls -la
                    echo 'Finish build steps'
                '''
            }
        }

        stage('Test') {
             agent {
                docker {
                    image 'node:19-alpine'
                    reuseNode true
                }
            }

            steps {
                sh '''
                    echo 'Test stage'
                    test -f ./build/index.html
                    npm test
                '''
            }
        }

        stage('E2e') {
             agent {
                docker {
                    image 'mcr.microsoft.com/playwright:v1.39.0-jammy'
                    reuseNode true
                }
            }

            steps {
                sh '''
                    npm install -g serve
                    serve -s build
                    npx playwright test
                '''
            }
        }
    }

    post {
        always {
            junit 'test-results/junit.xml'
        }
    }
}
