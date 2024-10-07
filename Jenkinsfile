pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/VS-Gowtham/CI-CD_Jenkins-app.git',
                    credentialsId: 'MY-GIT-Cred'
            }
        }
        stage('Build') {
            agent {
                docker {
                    image 'node:18-alpine'
                    reuseNode True
                }
            }
            steps {
                sh '''
                    npm --version
                    npm ci
                    npm run build
                    echo "Build is done"
                '''
            }
        }
        stage('Test') {
            agent {
                docker {
                    image 'node:18-alpine'
                    reuseNode True
                }
            }
            steps {
                sh '''
                    test -f build/index.html
                    npm test
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
