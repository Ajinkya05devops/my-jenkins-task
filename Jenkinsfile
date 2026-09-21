pipeline {
    agent any

    environment {
        APP_NAME = 'invoice-service'
        RELEASE_NOTES = 'Initial build'
    }

    stages {
        stage('Checkout') {
            steps {
                echo "App name: ${APP_NAME}"
                checkout scm
            }
        }
        stage('Build') {
            steps {
                echo "Notes: ${RELEASE_NOTES}"
                echo "Build started..."
                echo "Build success!"
            }
        }
        stage('Test') {
            steps {
                echo "Testing..."
                echo "Tests passed!"
            }
        }
        stage('Package') {
            when {
                branch 'main'
            }
            steps {
                echo "Packaging ${APP_NAME}"
            }
        }
    }

    post {
        success {
            echo "Build SUCCESS jhala!"
        }
        failure {
            echo "Build fail jhala"
        }
    }
}
