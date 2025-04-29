pipeline {
    agent { label 'ec2' }  // This tells Jenkins to run the pipeline on EC2 agent
    environment {
        PROJECT_NAME = 'MyProject'
    }
    stages {
        stage('Build') {
            steps {
                echo "Building ${env.PROJECT_NAME}"
                sh "docker build -t" 
                echo "Docker build completed successfully"
                echo "Build Stage Complete"
            }
        }
        stage('Test') {
            steps {
                echo "Running tests for ${env.PROJECT_NAME}"
                echo "Testing Completed"
            }
        }
        stage('Deploy') {
            steps {
                echo "Deploying ${env.PROJECT_NAME}"
                echo "Deploying Completed"
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
