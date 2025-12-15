pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                echo "Checking out branch: ${env.BRANCH_NAME}"
                checkout scm
            }
        }

        stage('Build') {
            steps {
                echo "Building branch: ${env.BRANCH_NAME}"
                // Compile Maven project
                sh 'mvn clean compile'
            }
        }

        stage('Test') {
            steps {
                echo "Running tests for branch: ${env.BRANCH_NAME}"
                // Run unit tests
                sh 'mvn test'
            }
        }

        stage('Deploy') {
            when {
                branch 'main'
            }
            steps {
                echo "Deploying application from main branch"
                // Optional deploy command
                // sh './deploy.sh'
            }
        }
    }

    post {
        success {
            echo "Pipeline SUCCESS for ${env.BRANCH_NAME}"
        }
        failure {
            echo "Pipeline FAILED for ${env.BRANCH_NAME}"
        }
    }
}
