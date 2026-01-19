pipeline {
    agent any

    parameters {
        string(name: 'BRANCH_NAME', defaultValue: 'main', description: 'Git branch to build')
    }

    stages {

        stage('Checkout Code') {
            steps {
                echo "Checking out branch: ${params.BRANCH_NAME}"
                git branch: "${params.BRANCH_NAME}",
                    url: 'https://github.com/vamsichilaka/Jenkins.git'
            }
        }

        stage('Build Artifact') {
            steps {
                sh '''
                mkdir -p artifacts
                cp index.html artifacts/index_$BUILD_NUMBER.html
                '''
            }
        }

        stage('Test Artifact') {
            steps {
                sh '''
                if [ -f artifacts/index_$BUILD_NUMBER.html ]; then
                  echo "TEST PASSED"
                else
                  echo "TEST FAILED"
                  exit 1
                fi
                '''
            }
        }

        stage('Archive Artifact') {
            steps {
                archiveArtifacts artifacts: 'artifacts/*.html'
            }
        }

        stage('Deploy') {
            steps {
                echo "Deploying based on branch: ${params.BRANCH_NAME}"
                sh '''
                 if [ "$BRANCH_NAME" = "dev" ]; then
                    echo "Deploying to DEV environment"
                    sudo cp artifacts/index_$BUILD_NUMBER.html /var/www/html/dev/index.html

                elif [ "$BRANCH_NAME" = "main" ]; then
                    echo "Deploying to PROD environment"
                    sudo cp artifacts/index_$BUILD_NUMBER.html /var/www/html/prod/index.html

                else
                 echo "No deployment for this branch"
                fi
                '''
            }
        }
    }
}
