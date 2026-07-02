pipeline {
    agent any 

    environment {
        // Defines the SonarQube server environment configured in Jenkins
        PATH= "/opt/maven/bin:$PATH"
    }

    stages {
        stage('build') {
            steps {
                dir('cloning') {// Pulls the latest code from your repository
                    sh 'mvn clear deploy'
                }
            }
        }

        stage('SonarQube Analysis') {
            environment {
                // Runs the analysis using your project keys
                scannerHome=tool 'sonarqube_server'
            }
            steps{
                withSonarQubeEnv('SonarQube') {
                    sh "${SCANNER_HOME}/bin/sonar-scanner"
                }
            }
        }
    }
}
