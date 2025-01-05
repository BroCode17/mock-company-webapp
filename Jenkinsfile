pipeline {
    agent any

    // Ensure the build can be run on any agent
    options {
        disableConcurrentBuilds()
        buildDiscarder(logRotator(numToKeepStr: '5'))
    }

    // Define stages for the build pipeline
    stages {
        stage('Checkout') {
            steps {
                // Checkout code from repository
                checkout scm
            }
        }

        stage('Build') {
            steps {
                // Build the project using Gradle wrapper
                sh './gradlew assemble'
            }
        }

        stage('Test') {
            steps {
                // Run tests using Gradle wrapper
                sh './gradlew test'
            }
            post {
                always {
                    // Publish test results
                    junit '**/build/test-results/test/*.xml'
                }
            }
        }
    }

    // Post-build actions
    post {
        success {
            echo 'Build succeeded!'
        }
        failure {
            echo 'Build failed!'
        }
    }
}