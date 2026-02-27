pipeline {
    agent any

    stages {
        stage('Hello') {
            steps {
                echo 'Привет от Jenkins и Просто Девопс!'
                echo 'Сегодняшняя дата:'
                sh 'date'
            }
        }

        stage('System Info') {
            steps {
                echo 'Информация о системе:'
                echo 'Операционная система:'
                sh 'uname -a'
                echo 'Текущая директория:'
                sh 'pwd'
                echo 'Список файлов:'
                sh 'ls -la'
            }
        }

        stage('Environment') {
            steps {
                echo "Build Number: ${env.BUILD_NUMBER}"
                echo "Job Name: ${env.JOB_NAME}"
                echo "Workspace: ${env.WORKSPACE}"
            }
        }
    }
}
