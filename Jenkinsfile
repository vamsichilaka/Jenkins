pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                echo 'Code already checked out from Git'
            }
        }

        stage('Deploy') {
            steps {
                sh '''
                echo "Deploying application..."
                sudo cp index.html /var/www/html/index.html
                '''
            }
        }
    }
}
