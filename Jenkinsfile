pipeline {
    agent any
    
    environment {
        PYTHON_PATH = 'C:\\Users\\My PC\\AppData\\Local\\Programs\\Python\\Python313;C:\\Users\\My PC\\AppData\\Local\\Programs\\Python\\Python313\\Scripts'
    }
    
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        
        stage('Build') {
            steps {
                bat '''
                set PATH=%PYTHON_PATH%;%PATH%
                pip install -r requirements.txt
                '''
            }
        }
        
        stage('SonarAnalysis') {
            environment {
                SONAR_TOKEN = credentials('sqp_ca23a9acaeefd1856d4542d3163c2f4d06d6b138')
            }
            steps {
                bat '''
                set PATH=%PYTHON_PATH%;%PATH%
               sonar-scanner.bat 
               -D"sonar.projectKey=gussing_game_jenkins_project" 
               -D"sonar.sources=." 
               -D"sonar.host.url=http://localhost:9000" 
               -D"sonar.token=sqp_ca23a9acaeefd1856d4542d3163c2f4d06d6b138"
               
                '''
            }
        }
    }

    post {
        success {
            echo 'Went well and good'
        }
        failure {
            echo 'Failed'
        }
    }
}
