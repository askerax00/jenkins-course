pipeline {
    agent any
    stages {
        stage('List Basics') {
            steps {
                script {
                    def environments = ['dev', 'staging', 'production']
                    echo "Size: ${environments.size()}"
                    environments.add('qa')
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
    }
}
