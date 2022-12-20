pipeline {
    agent any

    stages {
        stage('Deploy to ECS') {
            steps {
                ecsDeploy(
                    clusterName: 'App',
                    serviceName: 'appsvc',
                    taskDefinition: 'App',
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
