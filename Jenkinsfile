pipeline {
    agent any
    tools {
        jdk 'jdk17'
        maven 'M3'
    }
    parameters {
        string(name: 'RELEASE_NOTES', defaultValue: 'Initial release', description: 'Release notes for this build')
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
                echo "App Name: ${APP_NAME}"
                echo "Branch: ${env.GIT_BRANCH}"
                checkout scm
            }
        }
        stage('Build') {
            steps {
                echo "Notes: ${params.RELEASE_NOTES}"
                sh 'mvn clean compile'
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
                expression { return env.GIT_BRANCH ==~ /.*main.*/ }
            }
            steps {
                echo "Packaging main branch only"
                sh 'mvn package -DskipTests'
            }
        }
    }
}
