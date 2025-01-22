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
  agent none
  tools {
    maven 'Maven'
  }
  stages {
    stage('SCM') {
      checkout scm
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
          steps {
              script {
                  // Run SonarQube analysis
                  sh """
                      mvn sonar:sonar \
                      -Dsonar.projectKey=SonarQube \
                      -Dsonar.host.url=http://localhost:32768/ \
                      -Dsonar.login=squ_be2cae3ec1c5108055f1ffacf433c5a6155256dc
                  """
              }
          }
      }
  }
}