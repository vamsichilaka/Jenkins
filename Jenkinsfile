pipeline {
    agent any

    stages {
        stage('Hello') {
            steps {
                echo 'Hello from Jenkins Pipeline'
            }
        }

        stage('Read Code') {
            steps {
                sh 'ls -l'
                sh 'cat README.md'
            }
        }
    }
}
