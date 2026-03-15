pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                echo "Building application..."
                sleep 2
                echo "Build completed"
            }
        }
        stage('Test') {
            steps {
                echo "Running tests..."
                sleep 2
                echo "Tests passed"
            }
        }
        stage('Deploy to Production') {
            steps {
                input message: "Deploy to production?"
                echo "Deploying to production..."
                sleep 3
                echo "Deployment completed successfully"
            }
        }
        stage('Notify Team') {
            steps {
                input message: "Send notification to the team?", ok: "Send Notification"
                echo "Sending notification..."
                echo "Notification sent to team@company.com"
            }
        }
        stage('Deploy Strategy') {
            steps {
                script {
                    def strategy = input(
                        message: "Select deployment strategy",
                        parameters: [choice(name: 'STRATEGY', choices: ['rolling', 'blue-green', 'canary'], description: 'Choose your method')]
                    )
                    echo "Selected strategy: ${strategy}"
                    if (strategy == 'rolling') {
                        echo "Deploying with rolling update..."
                    } else if (strategy == 'blue-green') {
                        echo "Deploying with blue-green strategy..."
                    } else if (strategy == 'canary') {
                        echo "Deploying with canary release..."
                    }
                }
            }
        }

	stage('Approval with Timeout') {
            options {
                timeout(time: 2, unit: 'MINUTES')
            }
            steps {
                input message: "Approve within 2 minutes"
                echo "Approval received in time"
            }
        }
    }
}
