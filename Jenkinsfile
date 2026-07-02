pipeline {
    agent any 
    
    tools {
        jdk 'JAVA_HOME'
    }
    environment {
        // Defines the SonarQube server environment configured in Jenkins
        PATH= "/opt/maven/bin:$PATH"
    }

    stages {
        stage('build') {
            steps {
                dir('cloning') {// Pulls the latest code from your repository
                    sh 'mvn clean verify'
                }
            }
        }

        stage('SonarQube Analysis') {
            environment {
                // Runs the analysis using your project keys
                SCANNER_HOME = tool 'sonarqube_server'
            }
            steps{
                withSonarQubeEnv('sonarqube_server') {
                    sh "${SCANNER_HOME}/bin/sonarqube_server"
                }
            }
        }
    }
}
