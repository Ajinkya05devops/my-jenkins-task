pipeline {
    agent any
    tools {
        jdk 'jdk17'
        maven 'maven3'
    }
    parameters {
        string(name: 'RELEASE_NOTES', defaultValue: 'First release', description: 'Release notes liha')
    }
    environment {
        APP_NAME = 'invoice-service'
    }
    options {
        timeout(time: 15, unit: 'MINUTES')
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
                sh 'mvn compile'
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test'
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }
        stage('Package') {
            when {
                branch 'main'
            }
            steps {
                sh 'mvn package -DskipTests'
            }
        }
    }
    post {
        success { echo "Build pass jhala" }
        failure { echo "Build fail jhala" }
    }
}
