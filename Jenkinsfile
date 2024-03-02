pipeline {
    agent any
    stages {
        stage('Clean') {
            steps {
                // Clean the project
                sh 'mvn -B clean'
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
         stage('Build') {
            steps {
                // Build the project
                sh 'mvn build'
            }
        }
    }
}
