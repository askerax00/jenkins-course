pipeline {
    agent none
    stages {
        stage('Check Agent') {
            agent any
            steps {
                echo "Running on agent..."
                sh 'hostname'
                echo "Workspace path: ${env.WORKSPACE}"
                echo "Node name: ${env.NODE_NAME}"
            }
        }

        stage('Build Info') {
            agent any
            steps {
                echo "Build information..."
                echo "Build Number: ${env.BUILD_NUMBER}"
                echo "Build ID: ${env.BUILD_ID}"
                echo "Build URL: ${env.BUILD_URL}"
            }
        }

        stage('System Details') {
            agent any
            steps {
                echo "=== System Details Stage ==="
                sh 'uname -a'
                sh 'whoami'
                sh 'pwd'               
                sh 'ls -la'               
                sh 'free -h || echo "Memory check skipped"'
                sh 'date'
            }
        }

        // Возвращаем стейдж с конкретной меткой
        stage('Specific Agent') {
            agent { 
                label 'linux' 
            }
            steps {
                echo "Running on agent with label 'linux'"
                sh 'uname -a'
                echo "This stage successfully found a node with the 'linux' label."
            }
        }
    }
}
