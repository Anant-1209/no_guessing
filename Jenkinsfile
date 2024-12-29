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

   

        stage('Install Dependencies') {
            steps {
                bat '"C:\\Users\\My PC\\AppData\\Local\\Programs\\Python\\Python313\\python.exe" -m pip install -r requirements.txt'
            }
        }

        stage('SonarAnalysis') {
            environment {
                SONAR_TOKEN = credentials('sqp_e83ecb56cf0592bb9d09596b44c8735477f92236') // Ensure the correct credentials ID
            }
            steps {
                bat """
                set PATH="%PYTHON_PATH%;%SONAR_SCANNER_PATH%;%PATH%"
               sonar-scanner.bat 
               -D"sonar.projectKey=guessing_game_jenkin_pipeline" 
               -D"sonar.sources=." 
               -D"sonar.host.url=http://localhost:9000" 
               -D"sonar.token=sqp_22669b2637294d5a15d647262861d5f465b6e977"
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
