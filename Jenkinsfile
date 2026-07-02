pipeline {
    agent any
    
    tools {
        jdk 'JAVA_HOME'
    }

    environment {
        PATH = "/opt/maven/bin:$PATH"
    }

    stages {
        stage('Build') {
            steps {
                dir('cloning') {
                    sh 'mvn clean verify'
                }
            }
        }

        stage('SonarQube Analysis') {
            environment {
                SCANNER_HOME = tool 'sonarqube_server'
            }
            steps {
                dir('cloning') {
                    withSonarQubeEnv('sonarqube_server') {
                        sh '''
                        ${SCANNER_HOME}/bin/sonar-scanner \
                          -Dsonar.token=8c4633c070d7832b19740377879178127b98c1a9 \
                          -Dsonar.host.url=https://sonarcloud.io \
                          -Dsonar.organization=saidemy01 \
                          -Dsonar.projectKey=irctc \
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
