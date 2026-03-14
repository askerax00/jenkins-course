pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo "Building application..."
                sh '''
                    mkdir -p build
                    echo "Application binary" > build/app.jar
                '''
            }
        }

        stage('Test') {
            steps {
                echo "Running tests..."
                sleep 2
                echo "Tests completed"
            }
        }

        stage('Deploy') {
            steps {
                echo "Deploying application..."
                sleep 3
                echo "Deployment completed"
            }
            // Post-блок на уровне конкретного стейджа
            post {
                always {
                    echo "Deploy stage finished"
                    sh 'ls -la build/'
                }
            }
        }
    }

     
    post {
        always {
            echo "=== Post Actions ==="
            echo "Pipeline completed"
            sh 'date'
        }
        success {
            echo "✓ Build SUCCESS"
            echo "Build Number: ${env.BUILD_NUMBER}"
            echo "All stages passed successfully"
        }
        failure {
            echo "✗ Build FAILED"
            echo "Build Number: ${env.BUILD_NUMBER}"
            echo "Check console output for details"
        }
	cleanup {
            echo "=== Cleanup Phase ==="
            echo "Removing temporary files..."
            sh 'mkdir -p temp && rm -rf temp'
            echo "Cleanup completed"
        }
    }
}
