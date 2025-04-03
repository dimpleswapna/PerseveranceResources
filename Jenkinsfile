
pipeline {
    agent any

    environment {
        SONARQUBE_URL = 'http://http://http://3.110.207.58:9000/'
        SONARQUBE_CREDENTIALS = 'sonar'//172.31.13.17
    }
    tools {
        maven 'maven'  //maven-build-tool
    }
    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main', url:'https://github.com/dimpleswapna/PerseveranceResources.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean install' // Adjust for Gradle or other build tools
            }
        }

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('') { 
                    sh 'mvn sonar:sonar -Dsonar.projectKey=My-First-SonarQube-Project'
                }
            }
        }

        stage('Quality Gate') {
            steps {
                script {
                    timeout(time: 5, unit: 'MINUTES') {
                        def qg = waitForQualityGate()
                        if (qg.status != 'OK') {
                            error "Pipeline failed due to quality gate failure: ${qg.status}"
                        }
                    }
                }
            }
        }
    }
}
