// pipeline {
//   agent any
//   tools {
//       maven 'Maven'
//   }
//   stages {
//     stage("build") {
//       steps {
//         sh 'mvn -v'
//       }
//     }

//     stage("test") {
//       steps {
//         echo 'Running tests'
//       }
//     }

//     stage("deploy") {
//       steps {
//         echo 'Deploying application'
//       }
//     }
//   }
// }

pipeline {
    agent any
    tools {
        maven 'Maven'
    }

    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/SparkLeau/DevSecOps.git' // Use your Git repository URL
            }
        }
        
        stage('Clean') {
            steps {
                sh 'mvn clean'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn compile'
            }
        }

        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }

        stage('SonarQube Analysis') {
            environment {
                SONAR_HOST_URL = 'http://172.21.48.1:32768/' // Replace with your SonarQube URL
                SONAR_AUTH_TOKEN = credentials('SonarQube') // Store your token in Jenkins credentials
            }
            steps {
                sh 'mvn sonar:sonar -Dsonar.projectKey=sample_project -Dsonar.host.url=$SONAR_HOST_URL -Dsonar.token=$SONAR_AUTH_TOKEN'
            }
        }

    }
}