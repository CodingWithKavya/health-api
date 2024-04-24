def projectKey = 'codingwithkavya' // Replace with your SonarCloud project key
def branch = env.BRANCH_NAME ?: 'master' // Use branch name from environment or default to 'master'
def gitUrl = 'https://github.com/CodingWithKavya/health-api.git' // Replace with your Git repository URL

pipeline {
  agent any
  environment {
        SONAR_TOKEN = credentials('sonarcloud')
    }

  stages {
    stage('Checkout Code') {
      steps {
        git branch: branch, url: gitUrl
      }
    }
    
    stage('Code Analysis') {
      steps {
        script {
          // Set SonarCloud server URL and token as environment variables
          sh "export sonar.host.url=https://sonarcloud.io"
          sh "export SONAR_TOKEN=${env.SONAR_TOKEN}" // Replace with environment variable holding SonarCloud token

          // Define additional SonarCloud properties (optional)
          sh """
          echo 'sonar.sources=src/main/java' // Replace with path to your source code
          """
          
          // Run SonarCloud analysis
          sh 'mvn sonar:sonar'
        }
      }
    }
  }
}
