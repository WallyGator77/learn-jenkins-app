pipeline {
    agent any

    stages {
        stage('Build') {
            agnet {
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
    }
}
