pipeline {
    agent any

    stages {
        stage('Branch Info') {
            steps {
                echo "Building branch: ${env.BRANCH_NAME}"
            }
        }
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
        stage('Deploy') {
            when {
                branch 'main'
            }
            steps {
                echo "Deploying ${env.BRANCH_NAME} to production!"
            }
        }
    }

    post {
        success { echo 'Pipeline succeeded!' }
        failure { echo 'Pipeline failed.' }
    }
}