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
        stage('Deploy to ECS') {
            steps {
                ecsDeploy(
                    clusterName: 'App',
                    serviceName: 'appsvc',
                    taskDefinition: 'App:1',
                    region: 'us-east-1',
                    containerDefinitions: [
                        {
                            name: 'frontend',
                            image: 'public.ecr.aws/t6e7g0f9/app',
                            portMappings: [
                                {
                                    containerPort: 3000,
                                    hostPort: 3000
                                }
                            ]
                        },
                        {
                            name: 'backend',
                            image: 'public.ecr.aws/t6e7g0f9/backend',
                            portMappings: [
                                {
                                    containerPort: 8080,
                                    hostPort: 8080
                                }
                            ]
                        }
                    ]
                )
            }
        }
    }
}
