pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Execution assemble...'
                sh './sampleWebApp/gradlew assemble -p sampleWebApp/'
                archiveArtifacts 'sampleWebApp/build/libs/*.jar'
            }
        }
        stage('Unit Test') {
            steps {
                echo 'Execute unit test...'
                sh './sampleWebApp/gradlew test -p sampleWebApp/'
            }
            post {
                always {
                    junit "sampleWebApp/build/test-results/test/*.xml"
                    archiveArtifacts 'sampleWebApp/build/reports/tests/test/*'
                }
            }
        }
        stage('Sonarqube') {
            steps {
                echo 'Sonarqube'
                sh './sampleWebApp/gradlew sonarqube -p sampleWebApp'
            }
        }
    }
}