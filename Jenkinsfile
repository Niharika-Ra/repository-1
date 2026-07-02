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
                dir('cloning') {
                    withSonarQubeEnv('sonarqube_server') {
                        sh '''
                         ${SCANNER_HOME}/bin/sonar-scanner 
                          -Dsonar.token=8c4633c070d7832b19740377879178127b98c1a9
                          -Dsonar.host.url=https://sonarcloud.io/
                          -Dsonar.organization=saidemny01 \
                          -Dsonar.projectKey=saidermy01_irctc \
                          -Dsonar.projectName=irctc \
                          -Dsonar.sources=. \
                          -Dsonar.java.binaries=target/classes
                        '''
                }
            }
        }
    }
}
}
