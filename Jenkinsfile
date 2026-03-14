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
    }
    post {
        always {
            echo "=== Post Actions ==="
            echo "Pipeline completed"
            sh 'date'
        }
    }
}
