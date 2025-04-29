pipeline {
    agent { label 'ec2' }  // This tells Jenkins to run the pipeline on EC2 agent
    environment {
        PROJECT_NAME = 'agecalculator'
        ECR_REGISTRY = '253490784255.dkr.ecr.ap-south-1.amazonaws.com/agecalculator'
        ECR_REPOSITORY = 'agecalculator'
    }
    stages {
        stage('Build') {
            steps {
                echo "Building ${env.PROJECT_NAME}"
                sh "docker build -t ${PROJECT_NAME}:latest ."
                echo "Docker build completed successfully"
                echo "Build Stage Complete"
            }
        }
        stage('Push to ECR') {
            steps {
                script {
                    // log in to AWS ECR
                    // tag the docker image 
                    // Push the Docker image to ECR
                    sh '''
                    aws ecr get-login-password --region ap-south-1 | docker login --username AWS --password-stdin 253490784255.dkr.ecr.ap-south-1.amazonaws.com
                    docker tag agecalculator:latest 253490784255.dkr.ecr.ap-south-1.amazonaws.com/agecalculator:latest
                    docker push 253490784255.dkr.ecr.ap-south-1.amazonaws.com/agecalculator:latest
                    '''
                }
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
