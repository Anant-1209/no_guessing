pipeline {
    agent any

    environment {
        PYTHON_PATH = 'C:\\Users\\My PC\\AppData\\Local\\Programs\\Python\\Python313;C:\\Users\\My PC\\AppData\\Local\\Programs\\Python\\Python313\\Scripts'
        SONAR_SCANNER_PATH = 'C:\Program Files\sonar-scanner-6.2.1.4610-windows-x64\bin'
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                bat """
                set PATH=%PYTHON_PATH%;%PATH%
                pip install -r requirements.txt
                """
            }
        }

        stage('SonarAnalysis') {
            environment {
                SONAR_TOKEN = credentials('guessing_game_token')
            }
            steps {
                bat """
                set PATH=%PYTHON_PATH%;%SONAR_SCANNER_PATH%;%PATH%
                sonar-scanner.bat 
                -D"sonar.projectKey=gussing_game_jenkins_project" 
                -D"sonar.sources=." 
                -D"sonar.host.url=http://localhost:9000" 
                -D"sonar.login=%SONAR_TOKEN%"
                """
            }
        }
    }

    post {
        success {
            echo 'Pipeline executed successfully!'
        }
        failure {
            echo 'Pipeline failed!'
        }
    }
}
