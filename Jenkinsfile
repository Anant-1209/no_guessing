pipeline {
    agent any

    environment {
        PYTHON_PATH = 'C:\\Users\\My PC\\AppData\\Local\\Programs\\Python\\Python313;C:\\Users\\My PC\\AppData\\Local\\Programs\\Python\\Python313\\Scripts'
        SONAR_SCANNER_PATH = 'C:\\Program Files\\sonar-scanner-6.2.1.4610-windows-x64\\bin'
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Debug Python Installation') {
    steps {
        bat 'where python'
        bat 'python --version'
        bat 'pip --version'
    }
}


        stage('Build') {
            steps {
                bat """
                set PATH="%PYTHON_PATH%;%PATH%"
                pip install -r requirements.txt
                """
            }
        }

        stage('SonarAnalysis') {
            environment {
                SONAR_TOKEN = credentials('sqp_e83ecb56cf0592bb9d09596b44c8735477f92236') // Make sure the token is correct
            }
            steps {
                bat """
                set PATH="%PYTHON_PATH%;%SONAR_SCANNER_PATH%;%PATH%"
                sonar-scanner.bat 
                -Dsonar.projectKey=guessing_game_jenkins_project  // Corrected the typo
                -Dsonar.sources=. 
                -Dsonar.host.url=http://localhost:9000 
                -Dsonar.login=%SONAR_TOKEN%
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
