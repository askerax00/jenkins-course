pipeline {
    agent any
    environment {
        PROJECT_NAME = 'CloudStore'
        DEPLOY_ENVIRONMENT = 'staging'
        RUN_SECURITY_SCAN = 'true'
    }
    stages {
        stage('Initialization') {
            script {
                echo "Starting ${PROJECT_NAME} Pipeline"
                def services = ['auth-service', 'api-gateway', 'user-service', 'payment-service']
                env.SERVICES = services.join(',')
                echo "Services to build: ${env.SERVICES}"
            }
        }
        stage('Build Services') {
            script {
                def serviceList = env.SERVICES.split(',')
                for (service in serviceList) {
                    echo "Building ${service}..."
                    sh "mkdir -p build/${service}"
                    sh "touch build/${service}/app.jar"
                    sleep 1
                    echo "Build completed for ${service}"
                }
            }
        }
        stage('Unit Tests') {
            when {
                expression { return (env.BUILD_NUMBER.toInteger() % 2 != 0) }
            }
            steps {
                echo "Running unit tests for build ${env.BUILD_NUMBER}"
                sleep 2
                echo "Unit tests passed"
            }
        }
        stage('Integration Tests') {
            when {
                expression { return (env.BUILD_NUMBER.toInteger() % 2 == 0) }
            }
            steps {
                echo "Running integration tests for build ${env.BUILD_NUMBER}"
                sleep 2
                echo "Integration tests passed"
            }
        }
        stage('Security Scan') {
            when {
                environment name: 'RUN_SECURITY_SCAN', value: 'true'
            }
            steps {
                echo "Running security vulnerability scan..."
                sleep 3
                echo "Security scan completed - no vulnerabilities found"
            }
            post {
                always {
                    echo "Security scan stage finished"
                }
            }
        }
        stage('Deployment Approval') {
            when {
                expression { return (env.DEPLOY_ENVIRONMENT == 'production' || env.DEPLOY_ENVIRONMENT == 'staging') }
            }
            steps {
                script {
                    timeout(time: 5, unit: 'MINUTES') {
                        def userInput = input(
                            id: 'approval',
                            message: "Approve deployment to ${DEPLOY_ENVIRONMENT}?",
                            parameters: [
                                choice(name: 'DEPLOY_STRATEGY', choices: ['rolling', 'blue-green', 'canary'], description: 'Strategy'),
                                booleanParam(name: 'SEND_NOTIFICATIONS', defaultValue: true, description: 'Notifications')
                            ]
                        )
                        echo "Deployment strategy: ${userInput.DEPLOY_STRATEGY}"
                        echo "Send notifications: ${userInput.SEND_NOTIFICATIONS}"
                        env.DEPLOY_STRATEGY = userInput.DEPLOY_STRATEGY
                    }
                }
            }
        }
        stage('Deploy Services') {
            script {
                def envMap = [
                    'staging': ['stage1.example.com', 'stage2.example.com'],
                    'production': ['prod1.example.com', 'prod2.example.com', 'prod3.example.com']
                ]
                def servers = envMap[env.DEPLOY_ENVIRONMENT]
                def serviceList = env.SERVICES.split(',')
                
                for (server in servers) {
                    for (service in serviceList) {
                        echo "Deploying ${service} to ${server} using ${env.DEPLOY_STRATEGY} strategy"
                        sleep 1
                    }
                }
            }
        }
    }
    post {
        always {
            echo "=== Pipeline Execution Complete ==="
            echo "Total build time: ${currentBuild.durationString}"
        }
        success {
            echo "✓ Deployment SUCCESS"
            echo "Project: ${PROJECT_NAME}"
            echo "Environment: ${DEPLOY_ENVIRONMENT}"
            echo "All services deployed successfully"
            writeFile file: 'deployment-report.txt', text: "Project: ${PROJECT_NAME}\nEnv: ${DEPLOY_ENVIRONMENT}\nStatus: SUCCESS"
        }
        failure {
            echo "✗ Deployment FAILED"
            echo "Build Number: ${env.BUILD_NUMBER}"
            echo "Check logs at: ${env.BUILD_URL}"
            echo "Rolling back changes..."
        }
        cleanup {
            echo "Cleaning up temporary files..."
            echo "Cleanup completed"
        }
    }
}
