pipeline {
    agent any

    stages {
        stage('Build and push Docker images') {
            steps {
                docker.build('frontend:latest', 'frontend')
                docker.build('backend:latest', 'backend')
                docker.withRegistry('https://568373317874.dkr.ecr.region.amazonaws.com', 'aws-ecr-credentials') {
                    docker.image('frontend:latest').push()
                    docker.image('backend:latest').push()
                }
            }
        }
    }
}
