pipeline {
    agent any
    stages {
        stage('Prepare') {
            steps {
                echo "Preparing workspace..."
                sh 'mkdir -p build logs temp'
                echo "Directories created"
            }
        }
	
	stage('Build') {
            steps {
                echo "Building application..."
                sh 'echo "Build version: 1.0.0" > build/version.txt'
                sh 'date >> build/version.txt'
                echo "Build completed"
            }
        }

	stage('Verify') {
            steps {
                echo "Verifying build..."
                sh 'cat build/version.txt'
                sh 'ls -la build/'
                echo "Verification completed"
            }
        }

	stage('System Info') {
            steps {
                echo "=== System Information ===" // 1
                echo "Checking current user..."   // 2
                sh 'whoami'                       // sh 1
                echo "Checking disk space..."     // 3
                sh 'df -h .'                      // sh 2
                echo "Build Number: ${env.BUILD_NUMBER}" // 4
                echo "Job Name: ${env.JOB_NAME}"         // 5
                sh 'uptime'                       // sh 3
            }
         }
    }
}
