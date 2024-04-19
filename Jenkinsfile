pipeline {
    agent any
    tools {
        maven 'maven'
    }

    stages {
        stage('Git Checkout') {
            steps {
                checkout scmGit(branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/CodingWithKavya/health-api.git']])
                echo 'Git Checkout Completed'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('Sonarcloud') {
                    sh '''mvn clean verify sonar:sonar -Dsonar.projectKey=CodingWithKavya_health-api -Dsonar.projectName='CodingWithKavya' -Dsonar.host.url=https://sonarcloud.io/''' //port 9000 is default for sonar
                    echo 'SonarQube Analysis Completed'
                }
            }
        }
    }
}
