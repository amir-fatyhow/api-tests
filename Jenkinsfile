pipeline {
    agent any

    tools {
        nodejs 'NodeJS_Latest'
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Install Newman') {
            steps {
                sh 'npm install -g newman'
            }
        }

        stage('Run API Tests') {
            steps {
                sh 'newman run collection.json -e env.json --reporters cli,junit --reporter-junit-export report.xml'
            }
        }
    }

    post {
        always {
            junit 'report.xml'
        }
    }
}