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
    }
}
