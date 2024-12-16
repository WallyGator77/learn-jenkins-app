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
            steps {
                sh '''
                    echo 'Test stage'
                    test -f ./build/index.html
                    npm test
                '''
            }
        }
    }
}
