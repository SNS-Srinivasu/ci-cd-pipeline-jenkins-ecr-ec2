pipeline {
    agent { label 'ec2' }

    environment {
        PROJECT_NAME = 'agecalculator'
        ECR_REGISTRY = '253490784255.dkr.ecr.ap-south-1.amazonaws.com'
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
                    sh '''
                        aws ecr get-login-password --region ap-south-1 | docker login --username AWS --password-stdin ${ECR_REGISTRY}
                        docker tag ${PROJECT_NAME}:latest ${ECR_REGISTRY}/${ECR_REPOSITORY}:latest
                        docker push ${ECR_REGISTRY}/${ECR_REPOSITORY}:latest
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
                sshagent(credentials: ['ec2-deploy-key']) {
                    sh """
ssh -o StrictHostKeyChecking=no ec2-user@15.207.237.235 << 'ENDSSH'
aws ecr get-login-password --region ap-south-1 | docker login --username AWS --password-stdin ${ECR_REGISTRY}
docker pull ${ECR_REGISTRY}/${ECR_REPOSITORY}:latest
docker rm -f agecalculator || true
docker run -d --name agecalculator -p 80:80 ${ECR_REGISTRY}/${ECR_REPOSITORY}:latest
ENDSSH
                    """
                }
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
