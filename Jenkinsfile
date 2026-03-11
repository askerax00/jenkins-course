pipeline {
    agent any

    environment {
        DEPLOY_ENV = 'staging'
    }

    stages {
        stage('Build') {
            steps {
                echo "Building application..."
                echo "Current branch: ${env.BRANCH_NAME ?: 'N/A'}"
                sh 'git branch --show-current || echo "Not in a git repo"'
            }
        }

        stage('Deploy to Production') {
            when { branch 'main' }
            steps {
                echo "Deploying to production environment"
                echo "Branch: main - deployment allowed"
            }
        }

}
