pipeline {
    agent any

    environment {
        SCANNER_HOME = tool 'SonarScanner'
    }

    stages {
        stage('Clone Repo') {
            steps {
                git url: 'https://github.com/Hamza844/flipkart-mern.git', branch: 'master'
            }
        }

        stage('SonarQube Scan') {
            steps {
                withSonarQubeEnv('My Sonar') {
                    withCredentials([string(credentialsId: 'sonar-token', variable: 'SONAR_TOKEN')]) {
                        sh '''
                            ${SCANNER_HOME}/bin/sonar-scanner \
                            -Dsonar.projectKey=flipkart-mern \
                            -Dsonar.sources=. \
                            -Dsonar.host.url=http://34.202.228.82:9000 \
                            -Dsonar.login="$SONAR_TOKEN"
                        '''
                    }
                }
            }
        }
    }
}
