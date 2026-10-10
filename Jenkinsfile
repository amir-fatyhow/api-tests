pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // Jenkins сам подтянет код из репозитория, из которого запущен пайплайн
                checkout scm
            }
        }

        stage('Install Newman') {
            steps {
                sh 'npm install -g newman'
                sh 'npm install -g newman-reporter-htmlextra'
            }
        }

        stage('Run API Tests') {
            steps {
                sh 'newman run collection.json -e env.json --reporters cli,htmlextra,junit --reporter-junit-export report.xml'
            }
        }
    }

    post {
        always {
            // Публикуем JUnit-отчёт, чтобы Jenkins показал результаты тестов
            junit 'report.xml'
        }
    }
}