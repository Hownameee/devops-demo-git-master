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
                    source venv/bin/activate
                    pip install --upgrade pip
                    pip install pytest
                '''
            }
        }

        stage('Run Tests') {
            steps {
                sh '''
                    venv/bin/activate
                    pytest --junitxml=results.xml
                '''
            }
        }
    }
}