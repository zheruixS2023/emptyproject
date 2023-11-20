pipeline {
    agent any
    environment {
        // Define environment variables
        SONARQUBE_URL = credentials('sonarqube-url')
        SONARQUBE_TOKEN = credentials('sonarqube-token')
    }
    stages {
        stage('Checkout') {
            steps {
                // Add a checkout step for your code repository
                checkout scm
            }
        }
        stage('Build') {
            steps {
                echo 'Building..'
                // Include your build steps here. For example:
                // sh './build.sh'
            }
        }
        stage('Test') {
            steps {
                script {
                    // Using environment variables for SonarQube
                    sh "sonar-scanner \
                        -Dsonar.projectKey=14848project \
                        -Dsonar.sources=. \
                        -Dsonar.host.url=http://localhost:9000 \
                        -Dsonar.token=${SONARQUBE_TOKEN}"
                }
            }
        }
        stage('Post-Build Actions') {
            steps {
                // Add any post-build actions like notifications
                // emailNotification('your-email@example.com')
            }
        }
    }
    post {
        failure {
            // Actions to perform on failure
            echo 'Build or Test Failed. Check logs for details.'
        }
        success {
            // Actions to perform on success
            echo 'Build and Test Succeeded.'
        }
    }
}
