pipeline {
    agent any
    environment {
        SONAR_AUTH_TOKEN = credentials('sonar-token')  // Retrieves token from Jenkins credentials
    }
    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/akylgit/test.git'
            }
        }
        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('SonarQube') {
                    sh '''
                    sonar-scanner \
                    -Dsonar.login=$SONAR_AUTH_TOKEN
                    '''
                }
            }
        }
    }
}
