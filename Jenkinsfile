pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/akylgit/test.git'
            }
        }
        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('SonarQube') { // Must match Jenkins config
                    sh 'sonar-scanner -Dsonar.host.url=http://192.168.56.15:9000'
                }
            }
        }
    }
}
