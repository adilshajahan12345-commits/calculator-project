pipeline {
    agent any

    environment {
        MAVEN = tool 'Default Maven'
    }

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                sh "${MAVEN}/bin/mvn clean compile"
            }
        }

        stage('Test') {
            steps {
                sh "${MAVEN}/bin/mvn test"
            }
        }

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('SonarQube') {
                    sh "${MAVEN}/bin/mvn clean verify org.sonarsource.scanner.maven:sonar-maven-plugin:sonar -Dsonar.projectKey=calculator-project -Dsonar.projectName='calculator-project'"
                }
            }
        }
    }
}
