pipeline {
    agent any
    tools {
        jdk 'Jdk'
        maven 'Maven'
    }
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
                sh 'mvn -B package'
            }
        }
        stage('Docker Build') {
            steps {
                // Build Docker image
                sh 'docker build -t cheikhdev10/java_maven_221 .'
            }
        }
        stage('Docker Push') {
            steps {
                // Push Docker image to repository
                withCredentials([usernamePassword(credentialsId: 'dockerhub', usernameVariable: 'cheikhdev10', passwordVariable: 'Mbectemi@2022')]) {
                    sh 'docker login -u $DOCKER_USERNAME -p $DOCKER_PASSWORD'
                    sh 'docker push cheikhdev10/java_maven_221'
                }
            }
        }
    }
}
