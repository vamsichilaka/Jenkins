pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                echo 'Code checked out from GitHub'
                sh 'ls -l'
            }
        }

        stage('Test') {
            steps {
                echo 'Testing application files'
                sh '''
                if [ -f index.html ]; then
                  echo "index.html exists - TEST PASSED"
                else
                  echo "index.html missing - TEST FAILED"
                  exit 1
                fi
                '''
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying to Apache web server'
                sh '''
                sudo cp index.html /var/www/html/index.html
                sudo systemctl restart httpd
                '''
            }
        }
    }

    post {
        always {
            echo 'Cleaning workspace'
            cleanWs()
        }
    }
}
