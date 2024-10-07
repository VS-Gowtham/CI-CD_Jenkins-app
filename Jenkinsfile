pipeline {
    agent any

    stages {
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
                echo "Testing is done"
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
