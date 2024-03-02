pipeline {
    agent any
    stages {
        stage('Clean') {
            steps {
                // Clean the project
                sh 'mvn -B clean'
            }
        }
        stage('Build') {
            steps {
                // Build the project
                sh 'mvn -B -DskipTests package'
            }
        }
        stage('Test') { 
            steps {
                // Run tests
                sh 'mvn test' 
            }
            post {
                always {
                    // Publish test results
                    junit allowEmptyResults: true, testResults: '**/test-results/*.xml'
                }
            }
        }
    }
}
