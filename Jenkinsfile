pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Quality Check') {
            steps {
                withSonarQubeEnv('SonarQube Server') {
                    sh 'mvn sonar:sonar'
                }
            }
        }

        stage('Publish Quality Gate Result') {
            steps {
                timeout(time: 1, unit: 'HOURS') {
                    publishQualityGateResults()
                }
            }
        }
    }
}

