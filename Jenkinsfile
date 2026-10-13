pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Build') {
            steps {
                bat 'mvn clean compile'
            }
        }
        stage('Test') {
            steps {
                bat 'mvn test'
            }
        }
        stage('Package') {
            steps {
                bat 'mvn package -DskipTests'
            }
        }
        stage('Docker Build') {
            steps {
                bat 'docker build -t jenkins-lab:%BUILD_NUMBER% .'
            }
        }
        stage('Docker Run') {
            steps {
                bat 'docker run --rm jenkins-lab:%BUILD_NUMBER%'
            }
        }
    }

    post {
        success { echo 'Pipeline succeeded!' }
        failure { echo 'Pipeline failed.' }
    }
}