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

//      stage('SonarQube Analysis') {
//         steps {
//               git url: 'https://github.com/alkuinmelvin/node-multiplayer-snake.git'
//         }
//      }

   }
}
