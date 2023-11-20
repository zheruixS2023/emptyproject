pipeline {
    agent any
    stages {
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
                    echo 'Test..'
                    SonarQube
                    sh "sonar-scanner \
                        -Dsonar.projectKey=14848project \
                        -Dsonar.sources=. \
                        -Dsonar.host.url=http://localhost:9000 \
                        -Dsonar.token=7e98743f690e43fe94862887293858ab"

                }
            }
        }
        stage('Post-Build Actions') {
            steps {
                // Add any post-build actions like notifications
                echo 'Post-Build Actions'
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
