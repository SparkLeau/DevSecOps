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

pipeline	{
  agent none
  stages {
    stage("Build & Analyse avec SonarQube") {
      agent any
      steps {
        script {
          sh 'mvn clean package sonar:sonar'
        }
      }
    }
  }
}