pipeline {
    agent any

    environment{
        NETLIFY_SITE_ID = 'f6967460-968a-444e-890b-1bf65c300db2'
    }
    stages {
        stage('Build') {
            agent{
                docker{
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps {
                sh  '''
                    ls -la
                    node --version
                    npm --version
                    npm ci
                    npm run build
                    ls -la
                '''
            }
        }
       
       stage('Deploy') {
            agent{
                docker{
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps {
                sh  '''
                    npm install netlify-cli
                     netlify-cli --version
                     echo "Deploying to production. Site ID: $NETLIFY_SITE_ID"
                '''
            }
        }
         stage('Test'){
            agent{
                docker{
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps{
                sh '''
                    test -f build/index.html
                    npm test
                ''' 
            }
        }
    }
}
