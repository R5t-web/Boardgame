pipeline {
    agent any
    
    tools{
        maven'maven3'
        jdk'jdk17'
    }
    environment{
        SCANNER_HOME=tool'sonar-scanner'
    }

    stages {
        stage('CleanWorkspace') {
            steps {
                cleanWs()
            }
        }
        
        stage('Compile') {
            steps {
                sh 'mvn compile'
            }
        }
        
        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }
        
        stage('Sonar-Analysis') {
            steps {
                withSonarQubeEnv('sonar') {
                   sh '$SCANNER_HOME/bin/sonar-scanner -Dsonar.projectName=Game -Dsonar.projectKey=Gamekey \
                   -Dsonar.java.binaries=target'
                }
            }
        }
        
        stage('Build') {
            steps {
                sh 'mvn package'
            }
        }
    }
}
