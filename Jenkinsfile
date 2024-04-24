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
        
        stage('SonarCloud Scan') {
            steps {
                script {
                    def apiUrl = 'https://sonarcloud.io/api/'
                    def projectKey = 'codingwithkavya'
                    
                    def analysisParams = [
                        'projectKey': projectKey,
                        'name': 'Jenkins Build',
                        'branch': 'master', // Specify the branch you want to analyze
                        'token': env.SONAR_TOKEN
                    ]
                    
                    def response = httpRequest(
                        contentType: 'APPLICATION_JSON',
                        httpMode: 'POST',
                        requestBody: analysisParams,
                        url: apiUrl + 'ce/submit'
                    )
                    
                    if (response.status != 200) {
                        error "Failed to trigger SonarCloud analysis: ${response.status} - ${response.content}"
                    } else {
                        echo "SonarCloud analysis triggered successfully."
                    }
                }
            }
        }
    }
}
