pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                echo 'Code checked out'
                sh 'ls -l'
            }
        }

        stage('Build Artifact') {
            steps {
                echo 'Creating versioned artifact'
                sh '''
                mkdir -p artifacts
                cp index.html artifacts/index_$BUILD_NUMBER.html
                '''
            }
        }

        stage('Test Artifact') {
            steps {
                echo 'Testing artifact'
                sh '''
                if [ -f artifacts/index_$BUILD_NUMBER.html ]; then
                  echo "Artifact exists - TEST PASSED"
                else
                  echo "Artifact missing - TEST FAILED"
                  exit 1
                fi
                '''
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying artifact to Apache'
                sh '''
                sudo cp artifacts/index_$BUILD_NUMBER.html /var/www/html/index.html
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
