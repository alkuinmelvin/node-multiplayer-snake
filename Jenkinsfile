pipeline {
    agent {
      node  {
         label 'ubuntu-agent'
      }
    }
    tools {
        jdk "jdk11"
    }
    stages {
      stage('Prepare - Checkout code') {
         steps {
               checkout scm
         }
      }

      stage('SAST SNYK'){
      snykSecurity(
            failOnIssues: false, 
            snykInstallation: 'Snyk V2', 
            snykTokenId: 'my-snyk-token'
            // place other parameters here, syntax generated using pipeline script generator in Jenkins
      )
      }

//      stage('SonarQube Analysis') {
//         steps {
//               git url: 'https://github.com/alkuinmelvin/node-multiplayer-snake.git'
//         }
//      }

   }
}
