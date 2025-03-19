pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/akylgit/test.git'
            }
        }
        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('SonarQube') { 
                    sh """
                    docker run --rm \
                        -v \$(pwd):/usr/src \
                        sonarsource/sonar-scanner-cli \
                        -Dsonar.projectKey=test \
                        -Dsonar.sources=/usr/src \
                        -Dsonar.host.url=http://192.168.56.15:9000
                    """
                }
            }
        }
    }
}
