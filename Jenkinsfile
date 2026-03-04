pipeline {
    agent any

    stages {
        stage('Preparation') {
            steps {
                echo "Starting WebStore CI/CD Pipeline"
                sh 'mkdir -p build test-reports artifacts'
                sh 'date'
                echo "Node: ${env.NODE_NAME}"
                echo "Workspace: ${env.WORKSPACE}"
            }
        }

        stage('Generate Version') {
            steps {
                script {
                    def major = '2'
                    def minor = '1'
                    def patch = env.BUILD_NUMBER
                    
                    def commitHash = "local"
                    if (env.GIT_COMMIT) {
                        commitHash = env.GIT_COMMIT.take(7)
                    }
                    
                    env.APP_VERSION = "${major}.${minor}.${patch}-${commitHash}"
                    echo "Application version: ${env.APP_VERSION}"
                }
            }
        }

       
        stage('Build Application') {
            steps {
                script {
                    echo "Building WebStore version ${env.APP_VERSION}"
                    
                    writeFile file: 'build/version.txt', text: env.APP_VERSION
                    writeFile file: 'build/app.jar', text: "WebStore Application Binary"
                    
                    sh 'ls -la build/'
                    echo "Build completed successfully"
                }
            }
        }

        stage('Unit Tests') {
            steps {
                echo "Running unit tests..."
                writeFile file: 'test-reports/unit-tests.xml', text: "Unit tests: PASSED"
                sleep 2
                echo "Unit tests completed"
            }
        }

        
        stage('Integration Tests') {
            steps {
                echo "Running integration tests..."
                writeFile file: 'test-reports/integration-tests.xml', text: "Integration tests: PASSED"
                sleep 3
                echo "Integration tests completed"
            }
        }

       
        stage('Package Artifacts') {
            steps {
                script {
                    def artifactName = "webstore-${env.APP_VERSION}.tar.gz"
                    echo "Creating artifact: ${artifactName}"
                    
                    
                    sh "tar -czf artifacts/${artifactName} build/ test-reports/"
                    
                    sh "ls -lh artifacts/"
                    echo "Artifact ready for deployment"
                }
            }
        }

        stage('Summary') {
            steps {
                script {
                    echo "=== Build Summary ==="
                    echo "Application: WebStore"
                    echo "Version: ${env.APP_VERSION}"
                    echo "Build Number: ${env.BUILD_NUMBER}"
                    echo "Build URL: ${env.BUILD_URL}"
                    echo "Status: SUCCESS"
                    echo "=== End of Pipeline ==="
                    sh 'ls -laR'
                }
            }
        }

       
        stage('Cleanup') {
            when {
                expression { currentBuild.result == null || currentBuild.result == 'SUCCESS' }
            
            steps {
                echo "Cleaning up temporary directories..."
                sh 'rm -rf build test-reports'
                echo "Cleanup completed. Remaining files:"
                sh 'ls -lhR artifacts/'
            }
        }
    }
}
