pipeline {
    agent any
    environment {
        PROJECT_NAME = 'MyProject'
    }
    stages {
        stage('Build') {
            steps {
                echo "Building ${env.PROJECT_NAME}"
                echo "Build Complete"
            }
        }
        stage('Test') {
            steps {
                echo "Running tests for ${env.PROJECT_NAME}"
                echo "testing Completed"
            }
        }
        stage('Deploy') {
            steps {
                echo "Deploying ${env.PROJECT_NAME}"
                echo "Deploying completed"
            }
        }
    }
    post {
        success {
            echo 'Pipeline succeeded!'
        }
        failure {
            echo 'Pipeline failed!'
        }
    }
}
