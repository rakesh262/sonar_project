pipeline {
    agent any
    tools {
        jdk 'JDK:1.8'
        maven 'Maven:3.6.0'
    }

    environment {
        JAVA_HOME = "${jdk}"
    }

    stages {
        stage('Prepare') {
            steps {
                checkout scm
            }
        }

        stage('Test') {
            steps {
                bat 'mvn install'
            }
        }

        stage('QA') {
            steps {
                withSonarQubeEnv('sonar') {
                    script {
                        def scannerHome = tool 'sonarqube-scanner'
                        bat "${scannerHome}/bin/sonar-scanner"
                    }
                }
            }
        }
    }
}
