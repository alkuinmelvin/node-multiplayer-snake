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

      stage('SonarQube analysis') {
         environment {
            scannerHome = tool 'SonarQube-Scanner' // the name you have given the Sonar Scanner (in Global Tool Configuration)
         }
         steps {
            withSonarQubeEnv(installationName: 'SonarQube-Server') {  // name of SonarQube Server in Jenkins Configuration System
                  sh "${scannerHome}/bin/sonar-scanner -X"
            }
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
            sh 'docker build -t snake:latest .'
            sh 'docker tag snake alkuinmelvin/snake:latest'
                sh 'docker tag snake alkuinmelvin/snake:$BUILD_NUMBER'
         }
      }

      stage('Post-to-dockerhub') {
         steps{
            withDockerRegistry([ credentialsId: "alkuin_docker", url: "" ]) {
            sh  'docker push alkuinmelvin/snake:latest'
            sh  'docker push alkuinmelvin/snake:$BUILD_NUMBER'
            }
         }
      }

      stage('Pull-image-server') {
         steps{
            sh "docker-compose down"
            sh "docker-compose up -d"
         }	
      }
   }
}
