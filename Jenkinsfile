pipeline {
    agent any

    stages {
        stage('Variables Demo') {
            steps {
                script {
                    def appName = "MyApplication"
                    def port = 8080
                    def isProduction = false

                    echo "Application Name: ${appName}"
                    echo "Server Port: ${port}"
                    echo "Production Mode: ${isProduction}"
                }
            }
        }
	

	stage('String Operations') {
            steps {
                script {
                    def message = "Jenkins Pipeline Tutorial"
                    
                    echo "Original: ${message}"
                    echo "String Length: ${message.length()}"
                    echo "Uppercase: ${message.toUpperCase()}"
                    echo "Lowercase: ${message.toLowerCase()}"
                    
                    // Заменяем слово и выводим результат
                    def newMessage = message.replace("Tutorial", "Course")
                    echo "Modified: ${newMessage}"
                }
            }
        }


	stage('Build Version') {
            steps {
                script {
                    def major = '1'
                    def minor = '0'
                    def patch = env.BUILD_NUMBER
                    env.APP_VERSION = "${major}.${minor}.${patch}"
                    echo "Application version: ${env.APP_VERSION}"
                }
            }
        }

	stage('Display Version') {
            steps {
                script {
                    // Используем переменную, которую создали в прошлом стейдже
                    echo "Using version: ${env.APP_VERSION}"
                    
                    def imageName = "myapp:${env.APP_VERSION}"
                    echo "Docker image would be: ${imageName}"
                }
            }
        }

	stage('Jenkins Info') {
            steps {
                script {
                    echo "Build Number: ${env.BUILD_NUMBER}"
                    echo "Build ID: ${env.BUILD_ID}"
                    echo "Job Name: ${env.JOB_NAME}"
                    echo "Workspace: ${env.WORKSPACE}"
                    echo "Build URL: ${env.BUILD_URL}"
                }
            }
        }

	stage('Generate Config') {
   	     steps {
        	script {
            	    def config = """
app:
  name: ${env.APP_VERSION}
  port: 8080

build:
  number: ${env.BUILD_NUMBER}
  date: ${new Date()}
"""
            	    echo "Generated config:"
                    echo config

                    writeFile file: 'config.yaml', text: config
                    sh 'cat config.yaml'
                }
            }
        }
	
    }
}
