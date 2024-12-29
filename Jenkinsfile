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
                SONAR_TOKEN = credentials('sqa_c78048dd75096cd8baa2e583466a98c36706cf60')
            }
            steps {
                bat '''
                set PATH=%PYTHON_PATH%;%PATH%
               sonar-scanner.bat 
               -D"sonar.projectKey=sonar_pipeline_jenkins" 
               -D"sonar.sources=." 
               -D"sonar.host.url=http://localhost:9000" 
               -D"sonar.token=sqp_8e5d48752c7e32c8336fa25995cd3e752f21b28a"
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
