pipeline {
    agent any

    stages {
        stage('Variables Demo') {
            steps {
                script {
                    // Создаем переменные разных типов
                    def appName = "MyApplication"
                    def port = 8080
                    def isProduction = false

                    // Выводим их через интерполяцию строк
                    echo "Application Name: ${appName}"
                    echo "Server Port: ${port}"
                    echo "Production Mode: ${isProduction}"
                }
            }
        }
    }
}
