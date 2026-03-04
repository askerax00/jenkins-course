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
    }
}
