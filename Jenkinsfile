pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building the app'
                sh 'ls -l'
            }
        }

        stage('Test') {
            steps {
                echo 'Running tests'
                sh 'cat README.md | grep "Hello DevOps"'
            }
        }
    }
}
