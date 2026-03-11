pipeline {
    agent any

    stages {
        stage('List Basics') {
            steps {
                script {
                    def environments = ['dev', 'staging', 'production']
                    echo "First element: ${environments[0]}"
                    echo "Last element: ${environments[-1]}"
                    echo "Size: ${environments.size()}"
                    environments.add('qa')
                    echo "Updated size: ${environments.size()}"
                }
            }
        }

        stage('Deploy to Servers') {
            steps {
                script {
                    def servers = ['server1.example.com', 'server2.example.com', 'server3.example.com']
                    for (server in servers) {
                        echo "Deploying to ${server}"
                        sleep 1
                        echo "Deployment to ${server} completed"
                    }
                }
            }
        }

        stage('Configuration Map') {
            steps {
                script {
                    def config = [
                        'appName': 'MyWebApp',
                        'version': '2.0.0',
                        'port': 8080,
                        'environment': 'production'
                    ]
                    echo "App Name: ${config.appName}"
                    echo "Version: ${config.version}"
                    echo "Port: ${config.port}"
                    echo "Env: ${config.environment}"
                    echo "Map size: ${config.size()}"
                    config['region'] = 'us-east-1'
                    echo "Full Map: ${config}"
                }
            }
        }

	stage('Environment Variables') {
            steps {
                script {
                    def envVars = [
                        'DATABASE_URL': 'postgresql://db.example.com:5432/mydb',
                        'CACHE_URL': 'redis://cache.example.com:6379',
                        'LOG_LEVEL': 'info'
                    ]
                    envVars.each { key, value ->
                        echo "${key} = ${value}"
                    }
                }
            }
        }

	stage('Multi-Environment Deploy') {
            steps {
                script {
                    def deployments = [
                        'dev': ['dev1.example.com', 'dev2.example.com'],
                        'staging': ['stage1.example.com'],
                        'prod': ['prod1.example.com', 'prod2.example.com', 'prod3.example.com']
                    ]
                    deployments.each { envName, serverList ->
                        for (server in serverList) {
                            echo "Deploying to ${envName}: ${server}"
                        }
                    }
                }
            }
        }
	
	stage('Filter Environments') {
            steps {
                script {
                    def allEnvs = ['dev', 'test', 'staging', 'prod', 'backup']
                    def activeEnvs = allEnvs.findAll { it != 'backup' }
                    echo "Active environments:"
                    activeEnvs.each { echo it }
                }
            }
        }
    }
}
