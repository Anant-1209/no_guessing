// pipeline {
//     agent any

//     environment {
//         PYTHON_PATH = 'C:\\Users\\My PC\\AppData\\Local\\Programs\\Python\\Python313;C:\\Users\\My PC\\AppData\\Local\\Programs\\Python\\Python313\\Scripts'
//         SONAR_SCANNER_PATH = 'C:\\Program Files\\sonar-scanner-6.2.1.4610-windows-x64\\bin'
//     }

//     stages {
//         stage('Checkout') {
//             steps {
//                 checkout scm
//             }
//         }

//         stage('Build') {
//             steps {
//                 bat """
//                 set PATH="%PYTHON_PATH%;%PATH%"
//                 pip install -r requirements.txt
//                 """
//             }
//         }

//         stage('SonarAnalysis') {
//             environment {
//                 SONAR_TOKEN = credentials('guessing_project_pipeline') // Make sure the token is correct
//             }
//             steps {
//                 bat """
//                 set PATH="%PYTHON_PATH%;%SONAR_SCANNER_PATH%;%PATH%"
//                 sonar-scanner.bat 
//                 -Dsonar.projectKey=guessing_game_jenkins_project  // Corrected the typo
//                 -Dsonar.sources=. 
//                 -Dsonar.host.url=http://localhost:9000 
//                 -Dsonar.login=%SONAR_TOKEN%
//                 """
//             }
//         }
//     }

//     post {
//         success {
//             echo 'Pipeline executed successfully!'
//         }
//         failure {
//             echo 'Pipeline failed!'
//         }
//     }
// }
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
                SONAR_TOKEN = credentials('guessing_project_pipeline') // Ensure the correct token is used
            }
            steps {
                bat """
                set PATH=%PYTHON_PATH%;%SONAR_SCANNER_PATH%;%PATH%
                sonar-scanner.bat 
                -Dsonar.projectKey=guessing_game_jenkins_project
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
