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
               git url: 'https://github.com/alkuinmelvin/node-multiplayer-snake.git'
         }
      }
   }
}
