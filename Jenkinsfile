pipeline {
    agent {
      node  {
         label 'ubuntu-agent'
      }
    }
    def app
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
         steps{
         snykSecurity(
            failOnIssues: false, 
            snykInstallation: 'Snyk V2', 
            snykTokenId: 'my-snyk-token'
            // place other parameters here, syntax generated using pipeline script generator in Jenkins
            )
         }
      }

      stage('Build-and-Tag') {
         steps{
         /* This builds the actual image; synonymous to
         * docker build on the command line */
            app = docker.build("alkuinmelvin/snake")
        }
      }

      stage('Post-to-dockerhub') {
         steps{
            docker.withRegistry('https://registry.hub.docker.com', 'alkuin_docker') {
            app.push("latest")
            }
         }
      }

      stage('Pull-image-server') {
         steps{
            sh "docker-compose down"
            sh "docker-compose up -d"
         }	
      }
//      stage('SonarQube Analysis') {
//         steps {
//               git url: 'https://github.com/alkuinmelvin/node-multiplayer-snake.git'
//         }
//      }

   }
}
