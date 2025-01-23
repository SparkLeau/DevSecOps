pipeline {
    agent none
    tools {
        maven 'Maven'
    }
    stages {
	   stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/SparkLeau/DevSecOps.git' 
            }

        stage('Test SonarQube Connection') {
            steps {
                script {
                    sh 'ping -c 4 sonarqube'  
                    sh 'curl -v http://192.168.10.50:32768/'
                }
            }
        }
        stage('SCM') {
            steps {
                checkout scm
            }
        }
        stage("Build & Analyse avec SonarQube") {
            agent any
            steps {
                script {
                    sh 'mvn clean package sonar:sonar'
                }
            }
        }
	   stage('SonarQube Analysis') {
            environment {
                SONAR_HOST_URL = 'http://192.168.10.50:32768/' 
                SONAR_AUTH_TOKEN = credentials('SonarQube') 
            }
            steps {
                sh 'mvn sonar:sonar -Dsonar.projectKey=sample_project -Dsonar.host.url=$SONAR_HOST_URL -Dsonar.token=$SONAR_AUTH_TOKEN'
            }
        }


        stage("deploy & OWASP Dependency-Check") {
            agent any
            steps {
                dependencyCheck additionalArguments: '''
                -o './'
                -s './'
                -f 'ALL'
                --prettyPrint
                --purge''', odcInstallation: 'owasp-dependency'
                dependencyCheckPublisher pattern: 'dependency-check-report.xml'
            }
        }
    }
}
