pipeline {
    agent any
    stages {
        stage ('Build Backend') {
            steps {
                bat 'mvn clean package -DskipTests=true'
            }
        }
        stage ('Unit Tests') {
            steps {
                bat 'mvn test'
            }
        }
        stage ('Sonar Analysis') {
            environment {
                scannerHome = tool 'SONAR_SCANNER'
            }
            steps {
                withSonarQubeEnv('SONAR_LOCAL') {
                    bat "${scannerHome}/bin/sonar-scanner \
                    -Dsonar.projectKey=DeployBack \
                    -Dsonar.host.url=http://localhost:9000 \
                    -Dsonar.login=cf1e5f892a2c3a092b2b60dfe8eb2b615ea4c62c \
                    -Dsonar.java.binaries=target \
                    -Dsonar.coverage.exclusions=**/.mvn/**,**/src/test/**,**/model/**,**Application.java"
                }
            }
        }
    }
}
