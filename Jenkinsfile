pipeline {
    agent any
    
    environment {
        SONAR_TOKEN = credentials('sonarcloud')
    }
    
    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/CodingWithKavya/health-api.git', branch: 'master'
            }
        }
        
        stage('SonarQube Scan') {
            steps {
                script {
                    def scannerHome = tool 'SonarScanner'
                    withSonarQubeEnv('SonarCloud') {
                        sh "${scannerHome}/bin/sonar-scanner -Dsonar.projectKey=codingwithkavya -Dsonar.organization=CodingWithKavya -Dsonar.sources=src"
                    }
                }
            }
        }
    }
}
