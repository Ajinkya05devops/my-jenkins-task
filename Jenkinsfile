pipeline {
    agent any

    tools {
        jdk 'jdk17'
        maven 'maven3'
    }

    parameters {
        string(name: 'RELEASE_NOTES', defaultValue: 'Initial release', description: 'Release notes')
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
                echo "App: ${APP_NAME}"
                checkout scm
                echo "Git Branch is: ${env.GIT_BRANCH}"
            }
        }
        stage('Build') {
            steps {
                echo "Release Notes: ${params.RELEASE_NOTES}"
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
                expression { 
                    return env.GIT_BRANCH ==~ /.main./ 
                }
            }
            steps {
                echo "Packaging on main branch - ${env.GIT_BRANCH}"
                sh 'mvn package -DskipTests'
            }
        }
    }
    post {
        success { echo "SUCCESS!" }
        failure { echo "FAILED!" }
    }
}
