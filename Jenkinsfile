pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // Pulls code from your repository
                checkout scm
            }
        }

        stage('Setup Environment') {
            steps {
                sh '''
                    python3 -m venv venv
                    . venv/bin/activate
                    pip install --upgrade pip
                    pip install pytest
                    # If you have a requirements.txt, uncomment the next line
                    # pip install -r requirements.txt
                '''
            }
        }

        stage('Run Tests') {
            steps {
                sh '''
                    . venv/bin/activate
                    # Runs pytest and generates a JUnit XML report for Jenkins to read
                    pytest --junitxml=results.xml
                '''
            }
            post {
                always {
                    // This publishes the test results in the Jenkins UI
                    junit 'results.xml'
                }
            }
        }
    }

    post {
        failure {
            echo 'Tests failed! Please check the logs and results.xml.'
        }
        success {
            echo 'All tests passed successfully.'
        }
    }
}